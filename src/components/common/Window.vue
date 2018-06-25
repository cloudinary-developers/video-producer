<template>
  <div class="window" :class="{window: true, 'timeline': isTimeline}">

  <v-toolbar dense dark color="secondary">
    <slot name="window-header"></slot>
  </v-toolbar> 
    <div class="window__content">
      <slot name="window-content"></slot>
    </div>
  </div>
</template>

<style>
.window {
  height: 60vh;
  border-right: 1px solid #323a45;
}
.window__header {
  background-color: #323a45;
  max-height: 40px;
  box-shadow: 0 0 2px 0 rgba(0, 0, 0, 0.5);
  padding: 5px 10px 10px 5px;
}
.window__content {
  padding: 20px;
}
.timeline {
  height: 25vh;
}

</style>

<script>
export default {
  props: ['isTimeline']
}
</script>



