<template>
  <v-app dark>
    <nav-bar></nav-bar>
    <v-content>
      <HelloWorld/>
    </v-content>
    <v-footer fixed="fixed" app>
      <span>&ensp; &copy; 2017</span>
    </v-footer>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import NavBar from './components/common/NavBar';

export default {
  name: 'App',
  components: {
    HelloWorld,
    NavBar
  },
  data() {
    return {};
  }
};
</script>
