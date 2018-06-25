<template>
  <div class="track">
    <v-btn dark small fab color="primary" @click="generateURL">
      <v-icon>play</v-icon>Play</v-btn>
    <v-layout align-center justify-space-around>
      <v-layout row wrap class="trackGrid">
  
      <v-flex xs3 v-for="clip in clips" :key="clip.asset_info.public_id" draggable>
        <a @click="previewAsset(clip)">
          <img :src="createThumbnailImage(clip.asset_info.secure_url)" :alt="clip.asset_info.public_id" :title="clip.asset_info.public_id">
        </a>
      </v-flex>
      </v-layout>



    </v-layout>
  </div>
  
</template>

<script>
export default {
  name: 'storyboard',
  props: ['editedClip'],
  data: () => ({
    clips:[]
  }),
  mounted() {
    
  },
  watch:{
    editedClip(newData, oldData){
      this.clips.push(newData);
    },

  },
  methods: {

    createThumbnailImage(secure_url) {
      const url =  secure_url.replace('.mp4','.png').replace('.jpg','.png').
      replace('.mov','.png').replace('upload/','upload/w_160,h_90,c_thumb,ar_16:9,r_8/');
      return url;
    },
    previewAsset(clip) {
      console.log(clip);
      this.$emit('preview-click', clip);
    },

     generateURL() {
      
      const cl = new cloudinary.Cloudinary({ cloud_name: 'de-demo' });

      const transformations = [];


       const clip0_public_id = this.clips[0].asset_info.public_id;
       const clip0_option = this.clips[0].transformations[0];

       console.log(clip0_option);

      

      

       let transArr =  this.clips.map(function(clip){ 

               console.log(clip);

      const layer = clip.asset_info.public_id.replace(/\//g,":");
      const tranform = { width:400, overlay:`video:${layer}`, 
                startOffset:clip.trim_info.start_offset,  
                endOffset:clip.trim_info.end_offset};
            return tranform;
      });

       // transArr = transArr.reverse();
       //  transArr.shift();
       //  transArr.unshift({width:'400'});

        clip0_option.transformation = transArr;

       
     //  clip0_option.transformation.flags = "splice";

       const url = cl.url(clip0_public_id, clip0_option);
       console.log(url);
       window.open(url, '_blank');
               
    },
  

  }

};
</script>

<style>

.track {
  display: inline-block;
  text-align: center;
  vertical-align: center;
  float: left;
  border: dashed 2px #0071BA;
  min-height: 90px;
  min-width: 98vw;
}

</style>