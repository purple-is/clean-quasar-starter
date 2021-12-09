<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md">
      <div v-if="showUploadedImage">
        <div style="width: 800px">
          <div class="text-h5 q-mb-sm">original:</div>
          <div class="q-pb-md">{{`https://purpletest.b-cdn.net/${fileName}`}}</div>
          <q-img
            :src="`https://purpletest.b-cdn.net/${fileName}`"
            class="q-mb-md"
          />
          <div class="text-h5 q-py-md">generated from original:</div>
          <div v-if="query" class="q-pb-md">{{`https://purpletest.b-cdn.net/${fileName}?${query}`}}</div>
          <q-btn label="generate" class="h6 q-mb-md" color="primary" @click="generateModal = true" />
          <q-img
            v-if="query"
            :src="`https://purpletest.b-cdn.net/${fileName}?${query}`"
          />
        </div>
      </div>
      <div class="q-gutter-sm row items-start" v-show="!showUploadedImage">
        <q-uploader
          :url="`https://storage.bunnycdn.com/${storageZoneName}/${this.fileName}`"
          style="max-width: 500px"
          :headers="[{ name: 'Content-Type', value: 'application/octet-stream' }, { name: 'AccessKey', value: libraryApiKey }]"
          method="PUT"
          :send-raw="true"
          @added="fileAdded"
          @uploaded="showImage"
        />
      </div>
    </div>
    <q-dialog v-model="generateModal">
      <q-card>
        <q-card-section>
          <div class="text-h6">Generate</div>
        </q-card-section>
        <q-card-section class="q-pt-none">
          <q-checkbox v-model="fixSelection" val="width=150" label="width=150" />
          <q-checkbox v-model="fixSelection" val="?height=75" label="?height=75" />
          <q-checkbox v-model="fixSelection" val="aspect_ratio=1:1" label="aspect_ratio=1:1" />
          <q-checkbox v-model="fixSelection" val="quality=5" label="quality=5" />
          <q-checkbox v-model="fixSelection" val="sharpen=true" label="sharpen=true" />
          <q-checkbox v-model="fixSelection" val="blur=25" label="blur=25" />
          <q-checkbox v-model="fixSelection" val="crop=350,350,25,30" label="crop=350,350,25,30" />
          <q-checkbox v-model="fixSelection" val="crop=300,300&crop_gravity=southwest" label="crop=300,300&crop_gravity=southwest" />
          <q-checkbox v-model="fixSelection" val="flip=true" label="flip=true" />
          <q-checkbox v-model="fixSelection" val="flop=true" label="flop=true" />
          <q-checkbox v-model="fixSelection" val="brightness=15" label="brightness=15" />
          <q-checkbox v-model="fixSelection" val="saturation=-60" label="saturation=-60" />
          <q-checkbox v-model="fixSelection" val="hue=66" label="hue=66" />
          <q-checkbox v-model="fixSelection" val="gamma=25" label="gamma=25" />
          <q-checkbox v-model="fixSelection" val="contrast=20" label="contrast=20" />
          <q-checkbox v-model="fixSelection" val="auto_optimize=high" label="auto_optimize=high" />
        </q-card-section>
        <q-card-actions align="right">
          <q-btn flat label="generate" color="primary" @click="generate" />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </q-page>
</template>

<script>
import axios from 'axios'
const libraryApiKey = '5b1a4154-0ff8-423c-a265994d94a1-a5fc-408e'
const storageZoneName = 'purpletest'

export default {
  name: 'PageIndex',
  data () {
    return {
      libraryApiKey: libraryApiKey,
      storageZoneName: storageZoneName,
      showUploadedImage: false,
      interval: null,
      showStopRefreshingButton: true,
      fileName: '',
      generateModal: false,
      fixSelection: [],
      query: ''
    }
  },
  methods: {
    fileAdded (files) {
      this.fileName = files[0].name
    },
    showImage () {
      this.showUploadedImage = true
    },
    generate () {
      console.log(this.fixSelection)
      this.query = this.fixSelection.join('&')
      this.generateModal = false
    }
  }
}
</script>
