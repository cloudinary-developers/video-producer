<template>
  <div class="breadcrumbs">
      <v-breadcrumbs divider="/">
        <v-breadcrumbs-item
          v-for="item in items"
          :key="item.text"
          :disabled="item.disabled">
          {{ item.text }}
        </v-breadcrumbs-item>
      </v-breadcrumbs>
    </div>
</template>

<script>
export default {
  name: 'breadcrumbs',
  data: () => ({
    items: [
      {
        text: 'Projects',
        disabled: false
      },
      {
        text: '8Eight',
        disabled: false
      }
    ]
  })

};
</script>

<style>

.breadcrumbs {
 /* display: inline;
  float: right;*/
}

</style>