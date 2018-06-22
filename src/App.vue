<template>
  <v-app dark>
    <NavBar></NavBar>
    <v-content>
      <Home/>
    </v-content>
    <v-footer fixed="fixed" app>
      <span>&ensp; &copy; 2017</span>
    </v-footer>
  </v-app>
</template>

<script>
import Home from './components/Home';
import NavBar from './components/common/NavBar';
import Window from './components/common/Window';

export default {
  name: 'App',
  components: {
    Home,
    NavBar,
    Window
  },
  data() {
    return {};
  }
};
</script>

<style>
.content {
  margin-top: 2px;
}
</style>

