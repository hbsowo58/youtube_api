<template>
  <div id="app">
    <h1>My first project</h1>
    <header>
      <TheSearchBar @input-change="onInputChange" />
    </header>
    <section>
      <VideoDetail :video="selectedVideo"></VideoDetail>
      <VideoList :videos="videos" @select-video="onVideoSelect"/>
    </section>
  </div>
</template>

<script>
import axios from 'axios'
import TheSearchBar from '@/components/TheSearchBar'
import VideoList from '@/components/VideoList'
import VideoDetail from '@/components/VideoDetail'

// const API_KEY = 'AIzaSyBk01_cuehwAKu_yNhs6QyBLdO2IuwFuaI'
const API_KEY = process.env.VUE_APP_YOUTUBE_API_KEY
const API_URL = 'https://www.googleapis.com/youtube/v3/search'

export default {
  name: 'App',
  components: {
    TheSearchBar,
    VideoList,
    VideoDetail,
  },
  data:function(){
    return {
      inputValue: null,
      videos: [],
      selectedVideo:null,
    } 
  },
  methods:{
    onInputChange: function(inputText){
      this.inputValue = inputText

      const params = {
        key: API_KEY,
        part:'snippet',
        type:'video',
        q: this.inputValue
      }

      axios({
        method: 'get',
        url : API_URL,
        params
      })
        .then(res => {
          console.log(res)
          this.videos = res.data.items
          // this.selectedVideo = this.videos[0]
        })
        .catch(err => {
          console.log(err)
        })
    },
    onVideoSelect: function(video){
      this.selectedVideo = video
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
