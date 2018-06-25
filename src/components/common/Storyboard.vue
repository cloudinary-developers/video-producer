<template>
  <div class="track">
    <v-layout align-center justify-space-around>
      Drop Assets here
    </v-layout>
  </div>
  
</template>

<script>
export default {
  name: 'storyboard',
  props: ['trackClip'],
  data: () => ({
    clips: []
  }),
  mounted() {
    
  }

};
</script>

<style>

.track {
  display: inline-block;
  text-align: center;
  vertical-align: center;
  float: left;
  border: dashed 2px #0071BA;
  min-height: 90px;
  min-width: 98vw;
}

</style>