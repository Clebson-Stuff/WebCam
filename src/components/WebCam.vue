<template>
  <div class="WebCam">
      <button v-on:click="loadCamera()">Camera</button>
      <video autoplay="true" ref="Cam" id="webCamera"></video>
  </div>
</template>

<script>
export default {
  name: 'WebCam',
  props: {
    msg: String
  },methods:{
      loadCamera : function(){
            var video = this.$refs.Cam;
                video.setAttribute('autoplay', '');
                video.setAttribute('muted', '');
                video.setAttribute('playsinline', '');
            if  (navigator.mediaDevices.getUserMedia) {
                navigator.mediaDevices.getUserMedia({audio: false, video: {facingMode: 'user'}})
                .then(stream => {
                    video.srcObject = stream;
                })
                .catch(error => {
                    alert("Oooopps... Falhou :'(" + error);
                });
            }
      }
  }, mounted: function(){
        this.$nextTick(function () {
            this.loadCamera();
        });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
