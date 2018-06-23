<template>
  <div class="assetlist-container">
<!-- <p>  {{ resources }}</p> -->
    <v-container fluid grid-list-md>
    <v-layout row wrap>
      <v-flex xs2 v-for="item in resources" :key="item.public_id" draggable>
        <a @click="previewItem(item)">
          <img :src="createThumbnailImage(item)" :alt="item.public_id">
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
    resources: [],
    headers: [
        {
          text: 'public_id',
          align: 'left',
          sortable: false,
          value: 'public_id'
        },
        { text: 'Asset Type', value: 'resource_type' }
      ]
  }),
  methods: {
    previewItem(item){
      console.log(item);
    },
    createThumbnailImage(image){
      return image.secure_url.replace('.mp4','.jpg').
      replace('.mov','.jpg').replace('upload/','upload/w_100,h_100,c_fill,ar_2:3/');
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