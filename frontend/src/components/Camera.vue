<template lang="pug">
.camera
  video#video(ref="video", width="640", height="480", autoplay)
  .button(@click="photoSnapped")
    p Snap Photo
  canvas#canvas(ref="canvas", v-show="snapped", width="640", height="480")
</template>

<script>

export default {
  data() {
    return {
      snapped: false,
      context: null,
      image: null
    }
  },
  methods: {
    photoSnapped() {
      this.snapped = true
      this.context.drawImage(this.$refs.video, 0, 0, 640, 480)
      this.image = this.$refs.canvas.toDataURL("image/png")
      // eslint-disable-next-line
      console.log(this.image)
    }
  },

  mounted() {
    this.context = this.$refs.canvas.getContext('2d')
    if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
      navigator.mediaDevices.getUserMedia({ video: true }).then(stream => {
        this.$refs.video.srcObject = stream
        this.$refs.video.play()
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.camera {
    margin-top: 10px;
    display: flex;
    flex-direction: column;
}
.button {
  width: 120px;
  height : 50px;
  background-color: lightskyblue;
  border-radius: 5px;
  align-self: center;
  margin-top: 10px;
  margin-bottom: 10px;
  &:hover {
    cursor: pointer;
  }
}
#video {
    align-self: center;
}
#canvas {
    width: 640px;
    height: 480px;
    align-self: center;
}
</style>