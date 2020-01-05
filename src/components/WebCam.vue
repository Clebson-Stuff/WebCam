<template>
  <div ref="content" class="WebCam">
      <button v-on:click="takeSnapShot()" id="capture"></button>

      <video autoplay="true" ref="Cam" id="webCamera">
          
      </video>
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
      }, takeSnapShot : function(){
          var video = this.$refs.Cam;
          var canvas = document.createElement('canvas');
          canvas.width = video.width;
          canvas.height = video.height;
          var ctx = canvas.getContext('2d');
          ctx.drawImage(video, 0, 0, canvas.width, canvas.height);
          this.$refs.content.appendChild(canvas);

      }
  }, mounted: function(){
        this.$nextTick(function () {
            this.loadCamera();
        });
  }
}
</script>

<style scoped>
    #cam{
        height: 50px;
   
    }
    .WebCam{
        width: 50vh;
        height: 50vh;
        border:5px;
        border-style: solid;
        border-color: brown;
        display:inline-block;
        position:relative;
    }
    video{
        width: 100%;
        height: 100%;
    }
    #capture{
        display: block;
        bottom: 14vh;
        border-radius: 50%;
        min-width: 5vh;
        min-height: 5vh;
        height: 100px;
        width: 100px;
        max-width: 6vh;
        max-height: 6vh;
        background: red;
        bottom: 10vh;
        position:absolute;
        bottom:8vh;
        left:50%;
        -webkit-transform:translate3d(-50%, -50%, 0);
        -moz-transform:translate3d(-50%, -50%, 0);
        transform:translate3d(-50%, -50%, 0);
    }
</style>
