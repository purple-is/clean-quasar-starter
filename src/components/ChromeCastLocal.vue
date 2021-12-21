<template>
  <div>
    <h3 class="text-center">Chromecast Local</h3>
    <video
      ref="video"
      preload="auto"
      class="video-js full-width"
      data-setup='{ "fluid": "true" }'
    >
      <source src="../assets/hs_blues11_11.mp4" type="video/mp4" />
    </video>
  </div>
</template>

<script>
import videojs from "video.js";
import "video.js/dist/video-js.css";
import "@silvermine/videojs-chromecast/dist/silvermine-videojs-chromecast.css";
export default {
  name: "ChromeCastLocal",
  data() {
    return {
      player: null
    };
  },
  mounted() {
    this.player = videojs(this.$refs.video, {
      autoplay: false,
      controls: true,
      preload: "auto",
      techOrder: ["chromecast", "html5"],
      plugins: {
        chromecast: {
          addButtonToControlBar: true,
          metadata: {
            title: "Title For Chromecast",
            subtitle: "Subtitle For Chromecast"
          }
        }
      }
    });

    this.player.on("chromecastConnected", function() {
      console.log("connected");
    });
    this.player.on("chromecastDisconnected", function() {
      console.log("disconnected");
    });
  },
  beforeDestroy() {
    if (this.player) {
      this.player.dispose();
    }
    this.player = null;
  }
};
</script>
