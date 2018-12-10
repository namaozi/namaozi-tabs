<template>
  <div>
    <svg id="horizontal-tab" viewbox="0 0 1200 300" width="1200" height="300">

      <g v-for="string in [1,2,3,4,5,6]" class="horizontal-lines" stroke="darkgray" stroke-width="1.5" fill="none">
        <line x1="50" x2="1200" :y1="string * consts['STRING_INTERVAL'] + consts['STRING_OFFSET']"
              :y2="string * consts['STRING_INTERVAL'] + consts['STRING_OFFSET']"></line>
      </g>

      <rect class="horizontal-tab-judge-line" fill="rgba(207, 11, 117, 0.5)"
            :x="consts['JUDGE_LINE_OFFSET']" :y="consts['STRING_OFFSET']" width=20 height=210></rect>

      {{/* ここがメインの譜面 */}}
      <g class="horizontal-tab-notes" v-for="bar in scoreArray">

        {{/* 小節線 */}}
        <line stroke="lightgray" stroke-dasharray="5,5" stroke-width="1.5" fill="none"
              :x1="bar.index * consts['BAR_WIDTH']" y1=75 :x2="bar.index * consts['BAR_WIDTH']" y2=225></line>

        {{/* 1小節中の音符配列が bar['notes'] */}}
        {{/* notes には { 2: "B", 6: "F" } の形で入る */}}
        <g v-for="(notes, index) in bar['notes']" class="bar-notes">

          {{/* ex.) note: "B", string: 2 */}}
          <g v-for="(note, string) in notes" class="notes">
            <Note :x="bar.index * consts['BAR_WIDTH'] + (index + 0.5) * consts['NOTE_WIDTH']"
                  :y="string * consts['STRING_INTERVAL'] + consts['STRING_OFFSET']"
                  :r="consts['NOTE_RADIUS']"
                  :pitch="note"
                  :nth="parseInt(string, 10)"
                  :capo="capo"
                  :tuning="tuning">
            </Note>
          </g>
        </g>
      </g>
    </svg>
  </div>
</template>

<script>
  import Note from './fragments/Note';

  export default {
    components: {
      Note,
    },
    props: {
      scoreArray: Array,
      beats: Number,
      position: String,
      tuning: String,
      capo: Number,
    },
    data: function () {
      return {
        consts: {
          STRING_INTERVAL: 30,
          STRING_OFFSET: 45,
          JUDGE_LINE_OFFSET: 70,
          BAR_WIDTH: 210,
          NOTE_WIDTH: 210 / this.beats,
          NOTE_RADIUS: 15,
        }
      }
    },
  }
</script>
<style scoped>
  #horizontal-tab {
    background-color: mintcream;
    margin: 10px;
  }
</style>
