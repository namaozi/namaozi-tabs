<template>
  <g>
    <circle :cx="x"
            :cy="y"
            :r="r"></circle>
    <text :x="x - 7" :y="y + 7">{{realPitch}}</text>
  </g>
</template>

<script>
  export default {
    props: {
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
      // いまのところ11フレットまでしか対応できない
      // 実音 = pitch + capo
      realPitch: function () {
        const num = (this.capo + this.pitchToNumber[this.pitch]) % 12;
        return this.numberToPitch[num];
      }
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
</style>
