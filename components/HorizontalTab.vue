<template>
  <div>
    {{this.scoreArray}}
    <svg viewbox="0 0  300" width="300" height="300">
      <line x1=100 y1=100 x2=200 y2=200 stroke="black"></line>
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

      }
    }
  }
</script>
