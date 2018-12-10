<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"/>
        <VideoList :videos="videos"/>
    </div>
</template>

<script>
  import axios from 'axios';
  import SearchBar from '@/components/SearchBar';
  import VideoList from '@/components/VideoList';

  const API_KEY = 'AIzaSyD7t6yQQsvbEZIga5OtqFNrrp05qeXHdqw';

  export default {
    name: 'App',
    components: {SearchBar, VideoList},
    data() {
      return {
        videos: []
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
    },
  };
</script>

<style scoped>

</style>