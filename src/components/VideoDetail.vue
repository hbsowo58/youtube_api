<template>
    <div v-if="video" class="video-detail">
        <iframe :src="videoURI" frameborder="0"></iframe>
    </div>
</template>

<script>

export default {
  name: 'VideoDetail',
  props: {
      video: {
          type: Object,
      }
  },
  computed: {
      videoURI: function(){
          console.log(this.video)
          return `https://www.youtube.com/embed/${this.video.id.videoId}`
      }
  }
}
</script>


