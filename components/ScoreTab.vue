<template>
  <div>
    <Score :song="this.song" />
    <HorizontalTab />
    <VerticalTab />
  </div>
</template>

<script>
  import Score from '../components/Score';
  import HorizontalTab from '../components/HorizontalTab';
  import VerticalTab from '../components/VerticalTab';

  export default {
    components: {
      Score,
      HorizontalTab,
      VerticalTab,
    },
    props: {
      song: {
        type: Object,
        required: true,
        default: 'song', // 降ってくるsong
      },
    },
    data: function () {
      return {
        hoge: 'hoge',
      }
    }
  }
</script>
