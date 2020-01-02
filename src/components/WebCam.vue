<template>
  <div v-on:load="loadCamera()" class="WebCam">
      <button v-on:click="loadCamera()">Camera</button>
      <video autoplay="true" id="webCamera"></video>
  </div>
</template>

<script>
export default {
  name: 'WebCam',
  props: {
    msg: String
  },methods:{
      loadCamera : function(){
            var video = document.querySelector("webCamera");
                ///video.setAttribute('autoplay', '');
                //video.setAttribute('muted', '');
                //video.setAttribute('playsinline', '');
            if  (navigator.mediaDevices.getUserMedia) {
                // eslint-disable-next-line no-console
                console.log("Chegou aqui");

                navigator.mediaDevices.getUserMedia({audio: false, video: {facingMode: 'user'}})
                .then( function(stream) {
                    video.srcObject = stream;
                })
                .catch(error => {
                    alert("Oooopps... Falhou :'(" + error);
                });
            }
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
