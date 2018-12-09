<template>
  <div class="content is-small">
    {{song.score}}
  </div>
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
