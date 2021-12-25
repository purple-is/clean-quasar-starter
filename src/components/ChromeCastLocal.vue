<template>
  <div>
    <h3 class="text-center">Chromecast Local</h3>
    <video
      ref="video"
      preload="auto"
      data-setup='{ "fluid": "true" }'
      class="video video-js full-width"
      >
      <source src="../assets/hs_blues11_11.mp4" type="video/mp4" />
    </video>
  </div>
</template>
<script>
import videojs from "video.js";

export default {
  name: "ChromeCastLocal",
  data() {
    return {
      player: null
    };
  },
  mounted() {
    this.player = videojs(this.$refs.video, {
      controls: true,
      techOrder: ["chromecast", "html5"]
    });
    this.player.chromecast();
  },
  beforeDestroy() {
    if (this.player) {
      this.player.dispose();
    }
    this.player = null;
  }
};
</script>
