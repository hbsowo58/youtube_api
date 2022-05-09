<template>
    <ul>
        <VideoListItem v-for="video in videos" :key="video.id.videoId" :video="video" @select-video="onSelectVideo">
            {{video.snippet.title}}
        </VideoListItem>
    </ul>
</template>

<script>
import VideoListItem from '@/components/VideoListItem.vue'

export default {
    name: 'VideoList',
    components:{
        VideoListItem,
    },
    props: {
        videos: {
            type: Array,
            required: true,
        }
    },
    methods:{
        onSelectVideo: function(video){
            this.$emit('select-video', video)
        }
    }
}
</script>


