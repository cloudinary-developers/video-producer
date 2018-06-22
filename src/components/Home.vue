<template>
  <div>
    <v-layout row>
      <v-flex xs6>
        <Window>
          <template slot="window-header">
            <v-icon>photo_library</v-icon> &nbsp;<Breadcrumbs></Breadcrumbs>
          </template>
          <template slot="window-content">
            Lorem ipsum, dolor sit amet consectetur adipisicing elit. Aperiam placeat amet rerum, est aut animi dicta iste vero cumque iusto repellat quas nobis? Alias delectus quo enim sint, explicabo at.
          </template>
        </Window>
      </v-flex>
      <v-flex xs6>
        <Window>
          <template slot="window-header">
            <v-icon>burst_mode</v-icon> &nbsp;Now Playing
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
            <v-icon>timeline</v-icon> &nbsp;Timeline
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
export default {
  components: {
    Window,
    Breadcrumbs
  }
};
</script>

