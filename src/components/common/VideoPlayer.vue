<template>
  <div class="video-container">
 	<v-container fluid>
 	<div class="caption">
 	<span :text="timecode">{{ timecode }}</span>  <span text="timecode"> {{timecode}}</span>
 	</div>
  
  	<video controls="yes" autoplay="no" name="media" id="videoPlayerPreview">
  		<source :src="src" type="video/mp4">
  	</video>
    </v-container>
  </div>
</template>

<script>
export default {
  props: [ 'source','seektime','duration'],
  name: 'video-player',
  data: () => ({
  	timecode: {},
    video: {}, 
    resources: [],
    src: '',
    timecode:{},
    player: {},
  }),
  
  watch: {

   	timecode(newData, oldData){
   		console.log('Watching:', newData,oldData)
      this.seektime = newData.seektime;
      this.duration = newData.seektime;
    },

    // whenever question changes, this function will run
    source: function (newData, oldData) {
    	console.log('Watching:', newData,oldData)
    	this.src = newData;
    	let player = document.querySelector('#videoPlayerPreview');
    	player.src = newData;
    }
  },

  // methods: {
  	
  	
  // },
  	
  // 	// updateCurrentPlayHeadTime(){
  // 	// 	let player = document.querySelector('#videoPlayerPreview');
  // 	// 	console.log(player);
  // 	// 	this.currentTrackTime =  "00:11:00";
  // 	// }
  //   // previewItem(item){
  //   //   console.log(item);
  //   // },
  //   // createPreviewVideo(video){
  //   //   return video.secure_url.replace('.png','.mp4').
  //   //   replace('upload/','upload/w_100,h_100,c_fill,ar_2:3,r_14/');
  //   // }

  // },
  mounted(){
  this.player = document.querySelector('#videoPlayerPreview');
  this.src = this.source;
  //this.timecode = new Object({seektime:this.seektime, duration:this.duration, url:""});

  this.player.addEventListener('timeupdate',function(event){
  	 //  console.log(event)
  this.timecode = new Object({seektime:event.target.currentTime, duration: event.target.duration});
  	  // this.duration = event.target.duration;

 		console.log('> ',this.timecode);
    },false);



  }

};

</script>
   
<style>
 

</style>