<template>
  <div id="app">
    <button @click="generateVideo">Generate Video</button>
    <div v-if="loading">Loading...</div>
    <div v-if="videoUrl">
      <video :src="videoUrl" controls></video>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      loading: false,
      videoUrl: null,
    };
  },
  methods: {
    async generateVideo() {
      this.loading = true;

      try {
        const response = await axios.post(
          "http://localhost:8000/generate_video"
        );
        this.videoUrl = response.data.url;
      } catch (error) {
        console.error("Error generating video:", error);
      } finally {
        this.loading = false;
      }
    },
  },
};
</script>

<style>
#app {
  text-align: center;
  margin-top: 60px;
}

video {
  width: 100%;
  max-width: 600px;
  margin-top: 20px;
}
</style>
