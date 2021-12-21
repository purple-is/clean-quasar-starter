<template>
  <div>
    <h3 class="text-center">Chromecast Remote</h3>
    <video
      ref="video"
      preload="auto"
      data-setup='{ "fluid": "true" }'
      class="video-js full-width"
    ></video>
  </div>
</template>

<script>
import videojs from "video.js";
import "video.js/dist/video-js.css";
import "@silvermine/videojs-chromecast/dist/silvermine-videojs-chromecast.css";
export default {
  name: "ChromeCastRemote",
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
      },
      sources: [
        "https://f001.backblazeb2.com/file/purple-content/products/catalog/lsv_Santos_Portrait_Painting/media/lsv_Santos_Portrait_Painting_11.mp4"
      ]
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
