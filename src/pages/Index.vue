<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md">
      <div v-if="showVideo">
        <div style="position: relative; padding-top: 56.25%;">
          <iframe
            :src="`https://iframe.mediadelivery.net/embed/${libraryID}/${videoID}?autoplay=true&asdf=${videoKey}`"
            loading="lazy"
            style="border: none; position: absolute; top: 0; height: 100%; width: 100%;"
            allow="accelerometer; gyroscope; autoplay; encrypted-media; picture-in-picture;"
            allowfullscreen="true"
          />
        </div>
        <q-btn v-if="showStopRefreshingButton" color="white" text-color="black" label="Stop Refreshing" class="q-ma-lg full-width" @click="stopRefreshing"/>
      </div>
      <div class="q-gutter-sm row items-start">
        <q-uploader
          :url="`http://video.bunnycdn.com/library/${this.libraryID}/videos/${this.videoID}`"
          style="max-width: 500px"
          :headers="[{ name: 'Content-Type', value: 'application/*+json' }, { name: 'AccessKey', value: libraryApiKey }]"
          method="PUT"
          :send-raw="true"
          @added="createVideo"
          @uploaded="refreshIframe"
        />
      </div>
    </div>
  </q-page>
</template>

<script>
import axios from 'axios'
const libraryApiKey = 'bd9c1d6a-7e53-477a-8e908f3cbaa9-3337-4426'
const libraryID = 19390

export default {
  name: 'PageIndex',
  data () {
    return {
      libraryID: libraryID,
      libraryApiKey: libraryApiKey,
      videoID: '',
      showVideo: false,
      videoKey: 0,
      interval: null,
      showStopRefreshingButton: true
    }
  },
  methods: {
    createVideo (files) {
      axios({
        method: 'post',
        url: `http://video.bunnycdn.com/library/${libraryID}/videos`,
        headers: {
          'Content-Type': 'application/*+json',
          AccessKey: libraryApiKey
        },
        data: { title: files[0].name }
      }).then(response => {
        this.videoID = response.data.guid
      })
    },
    refreshIframe (info) {
      this.showVideo = true
      this.interval = setInterval(() => {
        this.videoKey++
      }, 2600)
    },
    stopRefreshing () {
      clearInterval(this.interval)
      this.showStopRefreshingButton = false
    }
  }
}
</script>
