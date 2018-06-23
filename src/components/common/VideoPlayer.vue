<template>
  <div class="video-container">
 	<v-container fluid>
  	<video controls="yes" autoplay="no" name="media">
  		<source src="http://res.cloudinary.com/de-demo/video/upload/du_11.5,q_auto,so_30,w_600/v1528932336/Capitol360/shorter-ar.mp4" type="video/mp4">
  	</video>
    </v-container>
  </div>
</template>

<script>
export default {
  // props: [ 'cl'],
  name: 'video-player',
  data: () => ({
    video: {}, 
    resources: []
  }),
  methods: {
    previewItem(item){
      console.log(item);
    },
    createPreviewVideo(video){
      return video.secure_url.replace('.png','.mp4').
      replace('upload/','upload/w_100,h_100,c_fill,ar_2:3,r_14/');
    }
    
  },
  mounted(){
    this.cl = cloudinary;
    var wsURL = "https://video-producer.cloudinary.auth0-extend.com/list-resources";
    axios
      .get(wsURL)
      .then(response => {
        console.log(response)
        this.resources = response.data;
      })
  }

};

</script>
   
<style>
 

</style>