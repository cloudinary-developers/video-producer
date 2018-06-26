<template>
  <div class="track">
    <v-btn dark small fab color="primary" @click="generateURL">
      <v-icon>movie</v-icon></v-btn>
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
      const clip0_option = this.clips[0].transformations;
      console.log(clip0_option);

      
  let t = [];
  
  let transArr =  this.clips.forEach((clip) => { 
  // if(i === 0){
        //     return;
        // }
      console.log(clip)
      const layer = clip.asset_info.public_id.replace(/\//g,":");
      let vlayer = `video:${layer}`
      const tranform = { 
                        width:400, 
                        overlay: vlayer, 
                        startOffset:clip.trim_info.start_offset,  
                        endOffset:clip.trim_info.end_offset 
                      }
                  // if(i === this.clips.length -1){
                  //   tranform.flags = "splice"
                  // }
            t.push(tranform);
  });

  console.log(`index `, t);      
      clip0_option.transformation = t;
      clip0_option.width = '400';
      clip0_option.crop = 'fill';
        

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