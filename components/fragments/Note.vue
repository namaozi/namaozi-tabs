<template>
  <svg class="note" :viewBox="passedViewBox">
    <circle :class="'fret-' + fret" :cx="x"
            :cy="y"
            :r="r">
    </circle>
    <text class="tab-digit" :x="x - 7" :y="y + 7">{{fret}}</text>
  </svg>
</template>

<script>
  export default {
    props: {
      passedViewBox: String,
      x: Number,
      y: Number,
      r: Number,
      pitch: String, // ABC記法の音
      nth: Number, // 弦番号
      capo: Number, // カポの番号
      tuning: String, // 曲のチューニング(6弦から)
    },
    data: function () {
      return {
        pitchToNumber: {
          'C': 0,
          'C#': 1,
          'D': 2,
          'D#': 3,
          'E': 4,
          'F': 5,
          'F#': 6,
          'G': 7,
          'G#': 8,
          'A': 9,
          'A#': 10,
          'B': 11,
        },
        numberToPitch: {
          0: 'C',
          1: 'C#',
          2: 'D',
          3: 'D#',
          4: 'E',
          5: 'F',
          6: 'F#',
          7: 'G',
          8: 'G#',
          9: 'A',
          10: 'A#',
          11: 'B',
        }
      }
    },
    computed: {
      /**
       * 何フレットを押さえるかを返す
       * なおrelative記法で書くのでcapoを考慮する意味はない
       * ex.) 5弦解放:A, pitch:B => 2
       */
      fret: function () {
        const open = this.tuning[6 - this.nth];
        const distance = this.pitchToNumber[this.pitch] - this.pitchToNumber[open];
        return distance < 0 ? distance + 12 : distance;
      },
      /**
       * pitchを実音に変換する
       * いまのところ11フレットまでしか対応できない
       * 実音 = pitch + capo
       * @returns String
       */
      realPitch: function () {
        const num = (this.capo + this.pitchToNumber[this.pitch]) % 12;
        return this.numberToPitch[num];
      },

      /**
       * capoを加味した開放弦の実音を得る
       * @returns String
       */
      openPitch: function () {
        const num = (this.capo + this.pitchToNumber[this.tuning[6 - this.nth]]) % 12;
        return this.numberToPitch[num];
      },
    },
    methods: {
      //
    }
  }
</script>

<style scoped>
  circle {
    fill: #CCC;
    stroke: #333;
  }

  /* TAB colors */
  .fret-0{
    fill: #cacfd1;
    stroke: #696969;
  }
  .fret-1{
    fill: #cce8ff;
    stroke: #7ca9cf;
  }
  .fret-2{
    fill: #7ce6fa;
    stroke: #2991a3;
  }
  .fret-3{
    fill: #a1f7cc;
    stroke: #1b995e;
  }
  .fret-4{
    fill: #97f48d;
    stroke: #1f9314;
  }
  .fret-5{
    fill: #e1f1bb;
    stroke: #62860f;
  }
  .fret-6{
    fill: #f0eaa1;
    stroke: #8e8d0e;
  }
  .fret-7{
    fill: #efd0b2;
    stroke: #946a0e;
  }
  .fret-8{
    fill: #eeb6ab;
    stroke: #94400d;
  }
  .fret-9{
    fill: #ecbebb;
    stroke: #99150b;
  }
  .fret-10{
    fill: #eab7e4;
    stroke: #940955;
  }
  .fret-11{
    fill: #e8b9e7;
    stroke: #8b0378;
  }
  .fret-12{
    fill: #d7afe7;
    stroke: #5c036c;
  }
  .fret-13{
    fill: #847a95;
    stroke: #2d0353;
  }
  .fret-14{
    fill: #acb0e5;
    stroke: #1a036e;
  }
  .fret-15{
    fill: #5e5f83;
    stroke: #0b012e;
  }
  .tab-digit{
    fill: midnightblue;
    font-size: 1.5rem;
  }

</style>
