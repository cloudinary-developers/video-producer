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
       <FileUploader folder="Projects/Cloudinary/8Eight" v-on:asset-upload="refreshList($event)"></FileUploader>
       <v-btn dark small fab color="primary" @click="refreshAssets">
      <v-icon>refresh</v-icon></v-btn>
          </template>
          <template slot="window-content">
            <AssetList ref="assetlist" v-on:preview-click="trimVideo($event)"></AssetList>
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
           <VideoPlayer id="videoPlayer" :source="source" :clip="clip" v-on:add-track="addToStoryBoard($event)"></VideoPlayer>
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
           <Storyboard ref="storyboardContainer" v-on:preview-click="trimVideo($event)"  :editedClip="editedClip"></Storyboard>
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
import Storyboard from './common/Storyboard';

export default {
  components: {
    Window,
    Breadcrumbs,
    FileUploader,
    AssetList,
    VideoPlayer,
    Storyboard
  }, 
  data() {
    return {
      clip: {},
      editedClip: {},
      source: ''
    };
  },
  methods: {

    refreshAssets: function() {
      this.$refs.assetlist.fetchAssets(); 
    },
    refreshList: function(assets){
      console.log(assets);
      // todo add toast to show what was added.
      this.$refs.assetlist.fetchAssets(); 
    },
    trimVideo: function(clip) {
      console.log(clip);
      this.source = clip.video_url;
      console.log(this.source);
      this.clip = clip;
    },
    addToStoryBoard: function(clip) {
      console.log('ADD TO STORYBOARD:', clip);
      this.editedClip = clip;
    }
  }
};
</script>

<style>

</style>

