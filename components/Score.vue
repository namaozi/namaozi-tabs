<template>
  <textarea class="textarea is-small">{{song.score}}</textarea>
</template>

<script>
  export default {
    props: {
      song: {
        type: Object,
        required: true,
      },
    },
  }
</script>
