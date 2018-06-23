<template>
  <div>
    <v-layout row>
      <v-flex xs6>
        <Window>
          <template slot="window-header">
      <v-icon>photo_library</v-icon>
      <v-toolbar-title class="white--text"> Media Bin </v-toolbar-title>
      <v-spacer></v-spacer>
      <Breadcrumbs></Breadcrumbs>
       <FileUploader></FileUploader>
          </template>
          <template slot="window-content">
            <AssetList v-on:preview-click="trimVideo($event)"></AssetList>
          </template>
        </Window>
      </v-flex>
      <v-flex xs6>
        <Window>
          <template slot="window-header">
            <v-icon>burst_mode</v-icon>
                  <v-toolbar-title class="white--text"> Now Playing </v-toolbar-title>
          </template>
          <template slot="window-content">
           <VideoPlayer id="videoPlayer" :source="source"></VideoPlayer>
          </template>
        </Window>
      </v-flex>
    </v-layout>
    <v-layout row wrap>
      <v-flex xs12>
        <Window :isTimeline="true">
          <template slot="window-header">
            <v-icon>timeline</v-icon>
            <v-toolbar-title class="white--text"> Timeline </v-toolbar-title>
          </template>
          <template slot="window-content">
            Lorem ipsum, dolor sit amet consectetur adipisicing elit. Aperiam placeat amet rerum, est aut animi dicta iste vero cumque iusto repellat quas nobis? Alias delectus quo enim sint, explicabo at.
          </template>
        </Window>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
import Window from './common/Window';
import Breadcrumbs from './common/Breadcrumbs';
import FileUploader from './common/FileUploader';
import AssetList from './common/AssetList';
import VideoPlayer from './common/VideoPlayer';
export default {
  components: {
    Window,
    Breadcrumbs,
    FileUploader,
    AssetList,
    VideoPlayer
  }, 
  // watch: {
  //   // whenever question changes, this function will run
  //   source: function (newData, oldData) {
  //     this.videoSource = newData;
  //   }
  // },
  data() {
    return {
      source: "https://res.cloudinary.com/de-demo/video/upload/du_11.5,q_auto,so_30,w_600/v1528932336/Capitol360/shorter-ar.mp4"
    };
  },
  methods: {
    trimVideo : function(url){
     

      this.source = url.replace('.mov','.mp4');
      console.log(this.source);
      
     // document.querySelector('#videoPlayer').src = this.source
      //alert(this.source);
    }
  }
};
</script>

<style>
 
</style>

