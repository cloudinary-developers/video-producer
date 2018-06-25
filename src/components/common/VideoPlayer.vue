<template>
<div class="video-container">
	<v-layout align-center justify-space-around>
  		<v-btn dark small fab color="primary" @click="previewClip">
	      <v-icon>view_array</v-icon>
	  	</v-btn>
      <v-btn dark small fab color="primary" @click="generateURL">
        <v-icon>add_to_queue</v-icon>
      </v-btn>
	</v-layout>
		<v-container align-center justify-space-around>
	  		<video ref="videoplayer" v-on:timeupdate="updateDisplay($event)" controls="yes" name="media" id="videoPlayerPreview">
  			</video>
	  	</v-container>

 	<v-layout align-center justify-space-around>
    
		<v-btn dark small fab color="primary" @click="trimStart" class="rotateLeft">
	      <v-icon>vertical_align_bottom</v-icon>
	  </v-btn>
		<v-spacer></v-spacer>
  	<div class="caption">
  		<span v-text="playheadPosition"></span> of <span v-text="duration"></span>
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
  props: ['source', 'clip'],
  name: 'video-player',
  data: function() {
    return {
      playheadPosition: 0,
      duration: 0,
      startoffset: 0,
      endoffset: 0,
      src: null,
      clips: [],
      currentClip: this.clip || {}
    }
  },

  methods: {
  	updateDisplay: function(event) {
  		this.playheadPosition = event.target.currentTime;
      this.duration = event.target.duration;
    },
    /*
    10 sec
    @2
    duration: 8
    startoffset: 2
    */
  	trimStart: function(event) {
      this.duration = this.duration - this.playheadPosition;
      this.startoffset = this.playheadPosition;
      this.endoffset = this.duration + this.playheadPosition;
    },
    /*
    10 sec
    @2
    duration: 8
    endoffset: 2
    */
  	trimEnd: function(event) {
      if (this.startoffset === 0) {
        this.duration = this.duration - this.playheadPosition;
        this.endoffset = this.duration;
        /*
        10
        start: 2
        end: 2
        duration: 6
        endoffset: 2
        */
      } else {
        this.duration = this.duration - this.playheadPosition - this.startoffset;
        this.endoffset = this.playheadPosition;
      }
    },
    generateURL: function() {
      this.currentClip.trim_info.start_offset = this.startoffset;
      this.currentClip.trim_info.end_offset = this.endoffset;
    
      const cl = new cloudinary.Cloudinary({ cloud_name: 'de-demo' });
      const public_id = this.currentClip.asset_info.public_id;
      const options = {
        duration: this.duration,
        endOffset: this.endoffset,
        startOffset: this.startoffset,
        resource_type: 'video',
        format: 'mp4'
      };

      const url = cl.url(public_id, options);
      // const player = this.$refs.videoplayer;
      // // player.src = url;
      // player.src = `${this.currentClip.video_url}#t=${this.startoffset},${this.endoffset}`;
      // player.play();

      this.currentClip.transformations = [];
      this.currentClip.transformations.push(options);
      this.currentClip.transformationVideoURL = url;

      this.clips.push(this.currentClip);
      console.log(this.clips);
    },
  	previewClip: function(event) {
      const player = this.$refs.videoplayer;
      player.src = `${this.currentClip.video_url}#t=${this.startoffset},${this.endoffset}`;
      player.play();
  	}
  },
  
  watch: {
    source: function(newUrl, oldUrl) {
      console.log('Watching:', newUrl, oldUrl);
      this.$refs.videoplayer.src = newUrl;

    },
    clip: function(newClip, oldClip) {
      this.currentClip = newClip;
    }
  },

  mounted() {
    this.seektime = 0;
    this.duration = 0;
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