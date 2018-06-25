<template>
  <div>
    <grid
  :draggable="true"
  :sortable="true"
  :items="items"
  :height="100"
  :width="100">
  <template slot="cell" slot-scope="props">
    <div>{{props.item}}</div>
  </template>
</grid>
  </div>
</template>

<script>
import Vue from 'vue'
import Grid from 'vue-js-grid' 
Vue.use(Grid)

export default {
  name: 'Track',
  components: { Container, Draggable },
  data () {
  return {
    items: [
      'a',
      'b',
      'c'
    ]
  }
}
};
</script>