<template>
  <div class="content is-large">
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
          title: 'shallowness',
          position: 'relative',
          tuning: 'EADGBE',
          capo: 2,
          beats: 5,
          score: `|6F,5C,4D,3G,5C|4D,5C,4D,3G,5C|6F,5C,4D,3G,5C|4D,5C,4D,3G,5C|
|6E,5C,4D,3G,5C|4D,5C,4D,3G,5C|6E,5C,4D,3G,5C|4D,5C,4D,3G,5C|
|6F,5C,4D,3G,5C|2B,5C,4D,3G,5C|6F,5C,4D,3G,5C|2B,5C,4D,3G,5C|
|6E,5C,4D,3G,5C|2B,5C,4D,3G,5C|6E,5C,4D,3G,5C|2B,5C,4D,3G,3A|
|[F;x;x;x;B;x],4D,3G,2C,5X|3A,5X,3A,3G,3A|[F;x;x;x;B;x],4D,3G,2C,5X|2D,  ,2C,2B,3G|
|[E;x;x;A;x;x],3G,3G,3G,5C|4D,5C,4D,3G,5C|6E,5C,4D,3G,5C|4D,5C,4D,3G,3A|
|[F;x;x;x;B;x],4D,3G,2C,5X|3A,5X,3A,3G,3A|[F;x;x;x;B;x],4D,3G,2C,5X|2D,  ,2C,2D,1E|
|[E;x;x;G;B;F],1E,1E,  ,5C|4D,5C,4D,3G,5C|[x;A;E;G;D;x],  ,2C,2C,6G|[x;x;D;G;B;x],  ,3G,  ,4D|
|6F,5C,4D,3G,5C|4D,5C,4D,3G,5C|6F,5C,4D,3G,5C|4D,5C,4D,3G,5C|
|6E,5C,4D,3G,5C|4D,5C,4D,3G,5C|6E,5C,4D,3G,5C|4D,5C,4D,3G,5C|
|6F,5C,4D,3G,5C|2B,5C,4D,3G,5C|6F,5C,4D,3G,5C|2B,5C,4D,3G,5C|
|6E,5C,4D,3G,5C|2B,5C,4D,3G,5C|6E,5C,4D,3G,5C|2B,5C,4D,3G,3A|
|[F;x;x;x;B;x],4D,3G,2C,5X|3A,5X,3A,3G,3A|[F;x;x;x;B;x],4D,3G,2C,5X|2D,  ,2C,2B,3G|
|[E;x;x;A;x;x],3G,3G,3G,5C|4D,5C,4D,3G,5C|6E,5C,4D,3G,5C|4D,5C,4D,3G,3A|
|[F;x;x;x;B;x],4D,3G,2C,5X|3A,5X,3A,3G,3A|[F;x;x;x;B;x],4D,3G,2C,5X|2D,  ,2C,2D,1E|
|[E;x;x;G;B;F],1E,1E,  ,5C|4D,5C,4D,3G,5C|[x;A;E;G;D;x],  ,2C,2C,6G|3G,3A,2B,[E;x;D;G;C;x],2D|
|[F;x;x;G;C;E],  ,[x;x;x;A;C;x],[x;x;x;A;C;x],6F|3A,4E,[x;x;x;A;C;x],4E,3A|
|[F;x;x;G;C;E],  ,[x;x;x;A;C;x],[x;x;x;A;C;x],6F|3A,2C,1E,1G,1F|
|[E;x;x;G;B;E],  ,[x;x;D;G;B;x],[x;x;D;G;B;x],6E|3G,4D,[x;x;x;G;B;x],4D,3G|
|[x;A;E;G;D;x],  ,2C,2C,6G|3G,3A,2B,[E,x,D,G,C,x],2D|
|[F;x;x;G;C;E],  ,[x;x;x;A;C;x],[x;x;x;A;C;x],6F|3A,4E,[x;x;x;A;C;x],4E,3A|
|[F;x;x;G;C;E],  ,[x;x;x;A;C;x],[x;x;x;A;C;x],6F|3A,2C,1E,1G,1F|
|[E;x;x;G;B;G],  ,2D,2D,6E|2B,3G,2D,  ,1G|
|[x;A;x;G;C;F],  ,1E,1E,6G|[x;x;D;G;B;x],  ,3G,  ,4D|
|6F,5C,4D,3G,5C|4D,5C,4D,3G,5C|6F,5C,4D,3G,5C|4D,5C,4D,3G,5C|
|6E,5C,4D,3G,5C|4D,5C,4D,3G,5C|6E,5C,4D,3G,5C|4D,5C,4D,3G,5C|
|6F,5C,4D,3G,5C|2B,5C,4D,3G,5C|6F,5C,4D,3G,5C|2B,5C,4D,3G,5C|
|6E,5C,4D,3G,5C|2B,5C,4D,3G,5C|6E,5C,4D,3G,5C|2B,5C,4D,3G,3A|`
        }
      }
    }
  }
</script>
