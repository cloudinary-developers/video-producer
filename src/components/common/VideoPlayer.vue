<template>
<div class="video-container">
	<v-layout align-center justify-space-around>
  		<v-btn dark small fab color="primary" @click="previewClip">
	      <v-icon>movie_creation</v-icon>
	  	</v-btn>
	</v-layout>
		<v-container align-center justify-space-around>
	  		<video  ref="videoplayer"  v-on:timeupdate="updateDisplay($event)"  controls="yes" autoplay="no" name="media" id="videoPlayerPreview">
  				<source :src="src" type="video/mp4">
  			</video>
	  	</v-container>

 	<v-layout align-center justify-space-around>
    
		<v-btn dark small fab color="primary" @click="trimStart" class="rotateLeft">
	      <v-icon>vertical_align_bottom</v-icon>
	  </v-btn>
		<v-spacer></v-spacer>
  	<div class="caption">
  		<span v-text="currenttime"></span>  of <span v-text="duration"></span>
 	</div>
 	<v-spacer></v-spacer>
	  
	   <v-btn dark small fab color="primary" @click="trimEnd" class="rotateRight">
	      <v-icon>vertical_align_top</v-icon>
	  </v-btn>
	<div>
<v-spacer></v-spacer>		
 	</div>   
  </v-layout>	
</div>
</template>

<script>
export default {
  props: [ 'source','timecode','value','asset'],
  name: 'video-player',
  data: () => ({
  	currenttime: 0,
  	duration: 0,
  	startoffset: 0,
  	endoffset: 0,
    video: {}, 
    resources: [],
    src: '',
    player: {},
  }),
  methods: {

  	updateDisplay: event => {
  		this.currenttime = event.target.currentTime;
  		this.duration = event.target.duration;
  	},
  	trimStart: event => {
  		this.startoffset = this.currenttime;
  	},
  	trimEnd: event => {
  		this.endoffset = this.currenttime;
  	},
  	previewClip: event => {
  		const player = document.querySelector('#videoPlayerPreview');
  		const template = `https://res.cloudinary.com/de-demo/video/upload/w_600,so_${this.startoffset},e0_${this.endoffset}/v1528907842/${asset.public_id}`
  		console.log(template);
  	}
  },
  
  watch: {

    // whenever question changes, this function will run
    source: (newData, oldData) => {
    	console.log('Watching:', newData,oldData)
    	this.src = newData;
    	const player = document.querySelector('#videoPlayerPreview');
    	player.src = newData;
    }
  },

  mounted() {
    this.seektime = 0
    this.duration = 0;
    this.player = document.querySelector('#videoPlayerPreview');
    this.src = this.source;
  }

};

</script>
   
<style>
 .rotateLeft{
  -webkit-transform: rotate(-90deg);
    -moz-transform: rotate(-90deg);
    -o-transform: rotate(-90deg);
    -ms-transform: rotate(-90deg);
    transform: rotate(-90deg);
}

 .rotateRight{
  -webkit-transform: rotate(-90deg);
    -moz-transform: rotate(-90deg);
    -o-transform: rotate(-90deg);
    -ms-transform: rotate(-90deg);
    transform: rotate(-90deg);
}

</style>