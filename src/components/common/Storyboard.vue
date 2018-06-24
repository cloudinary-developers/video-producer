<template>
  <div class="track">
    Drop Assets here
  </div>
  
</template>

<script>
export default {
  name: 'storyboard',
  data: () => ({
    tracks: []
  }),
  mounted(){
    
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