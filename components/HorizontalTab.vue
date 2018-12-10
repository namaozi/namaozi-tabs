<template>
  <div>
    <svg id="horizontal-tab" viewbox="0 0 1200 300" width="1200" height="300">
      <g v-for="string in [1,2,3,4,5,6]" class="horizontal-lines" stroke="darkgray" stroke-width="1.5" fill="none">
        <line x1="50" x2="1000" :y1="string * consts['STRING_INTERVAL'] + consts['STRING_OFFSET']" :y2="string * consts['STRING_INTERVAL'] + consts['STRING_OFFSET']"></line>
      </g>
      <rect id="vertical-judge-line" fill="rgba(207, 11, 117, 0.5)" :x="consts['JUDGE_LINE_OFFSET']" :y="consts['STRING_OFFSET']" width=20 height=210></rect>
    </svg>
  </div>
</template>

<script>
  export default {
    props: {
      scoreArray: Array,
    },
    data: function () {
      return {
        consts: {
          STRING_INTERVAL: 30,
          STRING_OFFSET: 45,
          JUDGE_LINE_OFFSET: 70,
        }
      }
    }
  }
</script>
<style scoped>
  #horizontal-tab {
    background-color: mintcream;
    margin: 10px;
  }
</style>
