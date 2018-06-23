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
            Lorem ipsum, dolor sit amet consectetur adipisicing elit. Aperiam placeat amet rerum, est aut animi dicta iste vero cumque iusto repellat quas nobis? Alias delectus quo enim sint, explicabo at.
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
            Lorem ipsum, dolor sit amet consectetur adipisicing elit. Aperiam placeat amet rerum, est aut animi dicta iste vero cumque iusto repellat quas nobis? Alias delectus quo enim sint, explicabo at.
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
export default {
  components: {
    Window,
    Breadcrumbs,
    FileUploader
  }
};
</script>

<style>
 
</style>

