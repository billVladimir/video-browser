<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"/>
        <div class="row">
            <VideoDetail :video="selectedVideo"/>
            <VideoList :videos="videos" @videoSelect="onVideoSelect"/>
        </div>
    </div>
</template>

<script>
  import axios from 'axios';
  import SearchBar from '@/components/SearchBar';
  import VideoList from '@/components/VideoList';
  import VideoDetail from '@/components/VideoDetail';

  const API_KEY = 'AIzaSyD7t6yQQsvbEZIga5OtqFNrrp05qeXHdqw';

  export default {
    name: 'App',
    components: {VideoDetail, SearchBar, VideoList},
    data() {
      return {
        videos: [],
        selectedVideo: null
      };
    },
    methods: {
      onTermChange(searchTerm) {
        axios.get('https://www.googleapis.com/youtube/v3/search', {
          params: {
            key: API_KEY,
            type: 'video',
            part: 'snippet',
            q: searchTerm,
          },
        }).then((res) => {
          this.videos = res.data.items;
        });
      },
      onVideoSelect(video) {
        this.selectedVideo = video;
      }
    },
  };
</script>

<style scoped>

</style>