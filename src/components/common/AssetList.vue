<template>
  <div class="assetlist-container">

    <v-container fluid grid-list-md>
      
      <div class="caption"><span :text="asset_list">{{asset_list}}</span></div>
      

    <v-layout row wrap class="imageGrid">
  
      <v-flex xs3 v-for="clip in resources" :key="clip.asset_info.public_id" draggable>
        <a @click="previewAsset(clip)">
          <img :src="createThumbnailImage(clip.asset_info.secure_url)" :alt="clip.asset_info.public_id" :title="clip.asset_info.public_id">
        </a>
      </v-flex>
      </v-layout>
    
  </v-container>
   
    
  </div>
</template>

<script>
export default {
  // props: [ 'cl'],
  name: 'asset-list',
  data: () => ({
    resource_type: {},
    asset_list: 'Videos: 0 Images: 0',
    resources: []
  }),
  watch: {
    // whenever question changes, this function will run
    resource_type(newData, oldData){
      this.asset_list = `Images: ${newData.image} Videos: ${newData.video}`;
    },

    source: (newData, oldData) => {
      console.log('Watching:', newData,oldData)
      this.src = newData;
      const player = document.querySelector('#videoPlayerPreview');
      player.src = newData;
    }
  },
  methods: {
    generateUUID() {
      function s4() {
        return Math.floor((1 + Math.random()) * 0x10000)
          .toString(16)
          .substring(1);
      }
      return s4() + s4() + '-' + s4() + '-' + s4() + '-' + s4() + '-' + s4() + s4() + s4();
    },
    previewAsset(clip) {
      this.$emit('preview-click', clip);
    },
    fetchAssets() {
      const wsURL = "https://video-producer.cloudinary.auth0-extend.com/list-resources";
      axios
      .get(wsURL)
      .then(response => {
        console.log(response.data)
        this.resource_type = response.data.aggregations.resource_type;
        console.log(`images: ${this.resource_type.image} videos: ${this.resource_type.video}`);
        /*
        clips = [{
          asset_info: {
            resources[0]
          },
          clip_id: uuid(),
          clip_type: 'video',
          thumbnail: createThumbnail(secure_url),
          transformation: [{
            trans1, trans2
          }],
          trim_info: {
            start_offset: 1,
            end_offset: 5,
            duration: 3
          },
          meta: {
            transcription_url: '',
            tags: ''
          }
        }];
        */
        const clips = response.data.resources.map(asset => {
          const clip = {
            clip_id: this.generateUUID(),
            video_url: this.createPreviewVideo(asset),
            asset_info: asset,
            trim_info: {
              start_offset: 0,
              end_offset: 0,
              duration: (asset.resource_type === 'video' )? asset.duration : null
            }  
          }
          return clip;
        });
        console.log(clips);
        this.resources = clips;
      })
    },

    displayResourceTypes() {
      return `Images: ${this.resource_type.image} Videos: ${this.resource_type.video}`;
    },
    previewItem(asset){
      console.log(asset);
      this.$emit('preview-click', this.createPreviewVideo(asset));
    },
    createThumbnailImage(secure_url) {
      const url =  secure_url.replace('.mp4','.png').replace('.jpg','.png').
      replace('.mov','.png').replace('upload/','upload/w_160,h_90,c_thumb,ar_16:9,r_8/');
      return url;
    },
    createVideoFromImage(asset) {
      console.log('createVideoFromImage')
      const sanitized = asset.public_id.replace(/\//g,":");
      const layer = `l_${sanitized}`;
      //l_Projects:Cloudinary:8Eight:IMG_1893
      const url = `https://res.cloudinary.com/de-demo/video/upload/w_400,ar_16:9,c_fill/du_5,so_0/a_0,ar_16:9,b_auto,c_lpad,g_center,${layer},w_400/Projects/black.mp4`
      return url;
    },

    // helper to create URL
    createPreviewVideo(asset) {
      if (asset.resource_type === 'image') {
        return this.createVideoFromImage(asset);
      } else if (asset.resource_type === 'video') {
       const url = asset.secure_url
        .replace('.png',' .mp4').replace('.jpg', '.mp4')
        .replace('upload/', 'upload/w_400,ar_16:9,c_fill/');
        return url;
      }
    }

  },
  mounted() {
    this.cl = cloudinary;
    this.fetchAssets();
  }

};

</script>
   
<style>
 
.imageGrid{
  overflow-y: auto;
  max-height: 400px;
  vertical-align: baseline;
}
</style>