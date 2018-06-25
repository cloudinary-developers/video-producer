<template>
  <div>
  <v-btn dark small fab color="primary" @click="showUploadWidget">
      <v-icon>backup</v-icon>
  </v-btn>
 </div>   
</template>

<script>
  //Projects/Cloudinary/8Eight

export default {
  props: ['folder'],
  name: 'fileuploader',
  data: () => ({
    items: []
  }),
  mounted () {
   //this.folder = 'Projects/Cloudinary/8Eight';
  },

  methods: {
    onUploaded: function(error,result) {
      this.$emit('asset-upload', result);
    },
    showUploadWidget: function(){
      cloudinary.openUploadWidget({ 
        cloud_name: 'de-demo',
        folder: this.folder,
        upload_preset: 'video-producer'}, this.onUploaded);
      }
  }
};
</script>

<style>
  #uw-container {margin-bottom: 20px;}
  #grep-container {
      margin: 20 auto;
      width:400px;
      border-radius: 5px;
      background-color: #f2f2f2;
      padding: 20px;
      display: none
  }
  #spinner {
      text-align: center;
      width: 50%;
      margin: 20 auto 20 auto;
      display: none
  }

  #video-container {
      position: relative;
      width: 100%;
  }

  video {
    margin: 20 auto 20 auto;
    display: block;
  }

  .drop-title{
    padding-left: 100px;
    display: inline-block;
  }

  .dropzone {
    min-height: 60px;
    border: dashed 2px #F4B21B;
  /* display: inline;
    float: right;*/
  }

</style>