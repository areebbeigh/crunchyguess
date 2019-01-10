<template>
  <canvas id="canvas" height="1138px" width="640px"></canvas>
</template>

<script>
export default {
  data () {
    return {
      backgroundSrc: "https://img1.ak.crunchyroll.com/i/spire2/157fbfab6ce5b67534ce44c310a3b6a21547077641_full.png",
      guessImage: { width: 175, height: 243 },
      guessImageCoordinates: [ [36,390], [234,390], [425,390], [36,661], [234,661], [425,661] ],
      canvas: null,
      ctx: null
    }
  },

  methods: {
    setupCanvas () {
      const canvas = document.getElementById("canvas")
      const ctx = canvas.getContext('2d')
      const background = new Image()
      background.src = this.backgroundSrc
      background.onload = function () {
        ctx.drawImage(background, 0, 0, canvas.width, canvas.height)
      }

      this.canvas = canvas
      this.ctx = ctx
    },

    generateImage (animu) {
      this.setupCanvas()
      console.log(animu)
      animu.forEach(anime => {
        const img = new Image()
        const coordinates = this.guessImageCoordinates[animu.indexOf(anime)]
        img.src = anime.posterImage.original
        
        img.onload = () => {
          console.log(`embedding ${img.src} at ${coordinates}`)
          this.ctx.drawImage(img, coordinates[0], coordinates[1], this.guessImage.width, this.guessImage.height)
        }
      })
    }
  },

  mounted () {
    this.$root.$on('generate', (animu) => {
      this.generateImage(animu)
    })
  }
}
</script>

<style>

</style>
