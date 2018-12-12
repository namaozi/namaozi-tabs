<template>
  <div class="content">
    <ScoreTab :song="this.song" />
  </div>
</template>

<script>
  import ScoreTab from '../components/ScoreTab';

  export default {
    components: {
      ScoreTab,
    },
    data: function () {
      return {
        song: {
          title: 'playground',
          position: 'relative',
          tuning: 'EADGBE',
          capo: 0,
          beats: 8,
          score: `|5C,3G,2C,1E,[x;x;E;G;C;G], ,1F,1E|4D,3A,2D,1E,[G;x;D;A;C;F], ,1E, |[A#;F;G#;C#;F;C], , ,|`
        }
      }
    }
  }
</script>
