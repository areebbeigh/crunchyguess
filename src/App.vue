<template>
  <v-app dark>
    <v-container>
      <v-layout>
        <v-flex xs12 md7 class="pa-3">
          <guess-list></guess-list>
        </v-flex>
        <v-flex xs12 md5>
          <app-canvas></app-canvas>
        </v-flex>
      </v-layout>
    </v-container>
  </v-app>
</template>

<script>
import AppCanvas from '@/components/AppCanvas'
import GuessList from '@/components/GuessList'

export default {
  name: 'App',
  components: {
    AppCanvas,
    GuessList
  },
  data () {
    return {
      //
    }
  }
}
</script>

<style>

</style>

