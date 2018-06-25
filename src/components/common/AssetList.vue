<template>
  <div class="assetlist-container">

    <v-container fluid grid-list-md>
      
      <div class="caption"><span :text="asset_list">{{asset_list}}</span></div>
      

    <v-layout row wrap class="imageGrid">
  
      <v-flex xs3 v-for="item in resources" :key="item.public_id" draggable>
        <a @click="previewItem(item)">
          <img :src="createThumbnailImage(item)" :alt="item.public_id" :title="item.public_id">
        <!-- <v-card draggable>
          <v-card-media 
            :src="createThumbnailImage(item)"
            height="100px">
            <v-container fill-height>
              <v-layout fill-height>
                <v-flex xs12 align-end flexbox>
              <p>{{item.secure_url}}</p>
                </v-flex>
              </v-layout>
            </v-container>
          </v-card-media>
          <v-card-actions>
            <span class="headline white--text" v-text="item.resource_type"></span>
          </v-card-actions>
        </v-card> -->
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

    source: function (newData, oldData) {
      console.log('Watching:', newData,oldData)
      this.src = newData;
      let player = document.querySelector('#videoPlayerPreview');
      player.src = newData;
    }
  },
  methods: {
    fetchAssets(){
      var wsURL = "https://video-producer.cloudinary.auth0-extend.com/list-resources";
      axios
      .get(wsURL)
      .then(response => {
        console.log(response.data)
        this.resource_type = response.data.aggregations.resource_type;
        console.log(`images: ${this.resource_type.image} videos: ${this.resource_type.video}`);
        this.resources = response.data.resources;
      })
    },

    displayResourceTypes(){
      return `Images: ${this.resource_type.image} Videos: ${this.resource_type.video}`;
    },
    previewItem(asset){
      console.log(asset);
      this.$emit('preview-click', this.createPreviewVideo(asset));
    },
    createThumbnailImage(asset){
      let url =  asset.secure_url.replace('.mp4','.png').replace('.jpg','.png').
      replace('.mov','.png').replace('upload/','upload/w_160,h_90,c_thumb,ar_16:9,r_8/');
      return url;
    },
    createVideoFromImage(asset){
      console.log('createVideoFromImage')
      let sanitized = asset.public_id.replace(/\//g,":");
      let layer = `l_${sanitized}`;
      //l_Projects:Cloudinary:8Eight:IMG_1893
      let url = `https://res.cloudinary.com/de-demo/video/upload/c_scale,h_400,w_600/du_5,so_0/a_0,ar_16:9,b_auto,c_lpad,g_center,h_400,${layer},w_600/v1529791058/Projects/black.mp4`
      return url 
    },

    createPreviewVideo(asset){
      console.log('Asset: ' , asset);
      if (asset.resource_type === 'image'){
        let url = this.createVideoFromImage(asset);
        let video = { url:url, starttime:0 , duration: 5 }
          console.log('createVideoFromImage',video);
          return video;
      }else if (asset.resource_type === 'video') {
       let duration = Math.floor(asset.duration);
       let url = asset.secure_url.replace('.png','.mp4').replace('.jpg','.mp4').
      replace('upload/',`upload/w_600,so_0,du_${duration}/`);
      let video = { url:url, starttime:0 , duration: duration }
          console.log(video);
          return video;
      }
    }
    
  },
  mounted(){
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