<template>
  <div class="video-container">
 	<v-container fluid>
  	<video controls="yes" autoplay="no" name="media" id="videoPlayerPreview">
  		<source :src="src" type="video/mp4">
  	</video>
    </v-container>
  </div>
</template>

<script>
export default {
  props: [ 'source'],
  name: 'video-player',
  data: () => ({
    video: {}, 
    resources: [],
    src: ''
  }),
   watch: {
    // whenever question changes, this function will run
    source: function (newData, oldData) {
    	console.log('Watching:', newData,oldData)
    	this.src = newData;
    	document.querySelector('#videoPlayerPreview').src = newData;
    }
  },

  methods: {
    // previewItem(item){
    //   console.log(item);
    // },
    // createPreviewVideo(video){
    //   return video.secure_url.replace('.png','.mp4').
    //   replace('upload/','upload/w_100,h_100,c_fill,ar_2:3,r_14/');
    // }

  },
  mounted(){
  this.src = this.source;
    // this.cl = cloudinary;
    // var wsURL = "https://video-producer.cloudinary.auth0-extend.com/list-resources";
    // axios
    //   .get(wsURL)
    //   .then(response => {
    //     console.log(response)
    //     this.resources = response.data;
    //   })
  }

};

</script>
   
<style>
 

</style>