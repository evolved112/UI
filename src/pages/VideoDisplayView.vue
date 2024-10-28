<template>
  <div class="video-player-view">
    <!-- Video Display (3/5 of the width) -->
    <div class="video-container">
      <h2>Video Player</h2>
      <div v-if="selectedVideoUrl">
        <video width="100%" height="auto" controls>
          <source :src="selectedVideoUrl" type="video/mp4" />
          Your browser does not support the video tag.
        </video>
      </div>
      <div v-else class="placeholder">
        <p>Please select a video from the list on the right.</p>
      </div>
    </div>

    <!-- Video List (2/5 of the width) -->
    <div class="video-list">
      <h2>Video List</h2>
      <ul>
        <li
          v-for="(video, index) in videoList"
          :key="index"
          @click="selectVideo(video.url)"
          class="video-list-item"
        >
          {{ video.name }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedVideoUrl: null, // To hold the selected video URL
      videoList: [], // The list of videos that will be dynamically populated
    };
  },
  mounted() {
    this.loadVideos();
  },
  methods: {
    selectVideo(url) {
    if (this.selectedVideoUrl === url) {
      this.selectedVideoUrl = null; // Reset if the same video is clicked
      this.$nextTick(() => {
        this.selectedVideoUrl = url; // Force re-selection
      });
    } else {
      this.selectedVideoUrl = url; // Set a different video URL directly
    }
  },
    loadVideos() {
      // Use require.context to load video files from the "src/assets/videos" folder
      const videoContext = require.context('@/assets/videos', false, /\.(mp4|webm|ogg)$/);

      // Create a list of videos by mapping over the context
      this.videoList = videoContext.keys().map((filePath) => {
        const name = filePath.split("/").pop(); // Extract the file name
        const url = videoContext(filePath); // Get the actual file URL

        return {
          name,
          url,
        };
      });
    },
  },
};
</script>

<style scoped>
.content {
  padding: 0;
}
/* Container for the overall view */
.video-player-view {
  display: flex;
  justify-content: space-between;
  padding: 0px 20px;
  box-sizing: border-box;
  height: 100vh;
}

/* Video Container (3/5 width) */
.video-container {
  flex: 3;
  padding-right: 20px;
}

.video-container h2 {
  margin-bottom: 10px;
}

.placeholder {
  background-color: white;
  padding: 20px;
  text-align: center;
}

/* Video List Container (2/5 width) */
.video-list {
  flex: 2;
  border-left: 1px solid #ddd;
  padding-left: 20px;
}

.video-list h2 {
  margin-bottom: 10px;
}

.video-list ul {
  list-style: none;
  padding: 0;
}

.video-list-item {
  cursor: pointer;
  padding: 10px;
  border: 1px solid #ddd;
  margin-bottom: 10px;
  transition: background-color 0.3s ease;
}

.video-list-item:hover {
  background-color: #f0f0f0;
}
</style>
