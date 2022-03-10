<template>
  <q-page>
    <div class="row full-width text-center">
      <div class="col-12 q-mt-xl text-h4 text-pink">welcome to the world's easiest game</div>
      <div class="col-12 q-py-xl text-h5 text-blue">by Bowen and Josh</div>
    </div>
    <div v-if="showResult" class="row full-width justify-center">
      <h1 class="text-blue text-bold">YOU WIN!</h1>
    </div>
    <div class="row justify-center">
      <q-btn
        @click="go"
        size="xl"
        color="green"
      >
        {{ buttonLabel }}
      </q-btn>
    </div>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      showResult: null,
      buttonLabel: ''
    }
  },
  created () {
    this.initGame()
  },
  methods: {
    initGame () {
      this.showResult = false
      this.buttonLabel = 'Start Game'
    },
    go() {
      console.log(this.showResult)

      if (this.showResult) {
        this.initGame()
      } else {
        this.showResult = true
        this.buttonLabel = 'Play Again'
      }
    }
  }
}
</script>
