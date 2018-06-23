<template>
  <v-toolbar app>
    <v-btn icon>
      <img src="https://res.cloudinary.com/christekh/image/upload/w_28/v1529615941/blue_bg_qh6qvg.png" alt="Logo">
    </v-btn>
    <div class="logo-divider"></div>
    <v-toolbar-title v-text="title"></v-toolbar-title>
    <v-spacer></v-spacer>
    <v-btn icon>
      <v-icon>archive</v-icon>
    </v-btn>
    <div class="logo-divider"></div>
    <v-btn icon>
      <v-icon>link</v-icon>
    </v-btn>
    <v-btn color="info">
      <v-icon>movie </v-icon> &ensp; Generate Movie
    </v-btn>
  </v-toolbar>
</template>

<script>
export default {
  name: 'nav-bar',
  data() {
    return {
      title: 'Cloudinary Video Producer'
    };
  }
};
</script>

<style>
.toolbar {
  background-color: #0e2f5a !important;
}
.toolbar__content {
  padding-left: 10px;
  padding-right: 10px;
}
.logo-divider {
  background-color: rgba(255, 255, 255, 0.1);
  width: 0px;
  height: 60%;
  margin-left: 10px;
}
</style>


