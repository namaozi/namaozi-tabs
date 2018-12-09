<template>
  <div class="container content is-large">
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
          pitch: 'relative',
          tuning: 'EADGBE',
          capo: 2,
          score: `
===intro===
|6F,5C,4D,3G,5C,4D,5C,4D,3G,5C|6F,5C,4D,3G,5C,4D,5C,4D,3G,5C|
|6E,5C,4D,3G,5C,4D,5C,4D,3G,5C|6E,5C,4D,3G,5C,4D,5C,4D,3G,5C|
|6F,5C,4D,3G,5C,2B,5C,4D,3G,5C|6F,5C,4D,3G,5C,2B,5C,4D,3G,5C|
|6E,5C,4D,3G,5C,2B,5C,4D,3G,5C|6E,5C,4D,3G,5C,2B,5C,4D,3G,3A|
===verse===
|[FxxxBx],4D,3G,2C,5X|3A,5X,3A,3G,3A|[FxxxBx],4D,3G,2C,5X|2D,  ,2C,2B,3G|
|[ExxAxx],3G,3G,3G,5C|4D,5C,4D,3G,5C|6E,5C,4D,3G,5C|4D,5C,4D,3G,3A|
|[FxxxBx],4D,3G,2C,5X|3A,5X,3A,3G,3A|[FxxxBx],4D,3G,2C,5X|2D,  ,2C,2D,1E|
|[ExxGBF],1E,1E,  ,5C|4D,5C,4D,3G,5C|[xAEGDx],  ,2C,2C,6G|[xxDGBx],  ,3G,  ,4D|
===intro===
|6F,5C,4D,3G,5C,4D,5C,4D,3G,5C|6F,5C,4D,3G,5C,4D,5C,4D,3G,5C|
|6E,5C,4D,3G,5C,4D,5C,4D,3G,5C|6E,5C,4D,3G,5C,4D,5C,4D,3G,5C|
|6F,5C,4D,3G,5C,2B,5C,4D,3G,5C|6F,5C,4D,3G,5C,2B,5C,4D,3G,5C|
|6E,5C,4D,3G,5C,2B,5C,4D,3G,5C|6E,5C,4D,3G,5C,2B,5C,4D,3G,3A|
===verse===
|[FxxxBx],4D,3G,2C,5X|3A,5X,3A,3G,3A|[FxxxBx],4D,3G,2C,5X|2D,  ,2C,2B,3G|
|[ExxAxx],3G,3G,3G,5C|4D,5C,4D,3G,5C|6E,5C,4D,3G,5C|4D,5C,4D,3G,3A|
|[FxxxBx],4D,3G,2C,5X|3A,5X,3A,3G,3A|[FxxxBx],4D,3G,2C,5X|2D,  ,2C,2D,1E|
|[ExxGBF],1E,1E,  ,5C|4D,5C,4D,3G,5C|[xAEGDx],  ,2C,2C,6G|3G,3A,2B,[ExDGCx],2D|
===chorus===
|[FxxGCE],  ,[xxxACx],[xxxACx],6F|3A,4E,[xxxACx],4E,3A|
|[FxxGCE],  ,[xxxACx],[xxxACx],6F|3A,2C,1E,1G,1F|
|[ExxGBE],  ,[xxDGBx],[xxDGBx],6E|3G,4D,[xxxGBx],4D,3G|
|[xAEGDx],  ,2C,2C,6G|3G,3A,2B,[ExDGCx],2D|
|[FxxGCE],  ,[xxxACx],[xxxACx],6F|3A,4E,[xxxACx],4E,3A|
|[FxxGCE],  ,[xxxACx],[xxxACx],6F|3A,2C,1E,1G,1F|
|[ExxGBG],  ,2D,2D,6E|2B,3G,2D,  ,1G|
|[xAxGCF],  ,1E,1E,6G|[xxDGBx],  ,3G,  ,4D|
===intro===
|6F,5C,4D,3G,5C,4D,5C,4D,3G,5C|6F,5C,4D,3G,5C,4D,5C,4D,3G,5C|
|6E,5C,4D,3G,5C,4D,5C,4D,3G,5C|6E,5C,4D,3G,5C,4D,5C,4D,3G,5C|
|6F,5C,4D,3G,5C,2B,5C,4D,3G,5C|6F,5C,4D,3G,5C,2B,5C,4D,3G,5C|
|6E,5C,4D,3G,5C,2B,5C,4D,3G,5C|6E,5C,4D,3G,5C,2B,5C,4D,3G,3A|`
        }
      }
    }
  }
</script>
