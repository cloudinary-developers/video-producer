<template>
  <div class="window" :class="{window: true, 'timeline': isTimeline}">
    <div class="window__header">
      <slot name="window-header"></slot>      
    </div>
    <div class="window__content">
      <slot name="window-content"></slot>
    </div>
  </div>
</template>

<style>
.window {
  height: 55vh;
  border-right: 1px solid #323a45;
}
.window__header {
  background-color: #323a45;
  box-shadow: 0 0 2px 0 rgba(0, 0, 0, 0.5);
  padding: 5px 10px;
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



