<template>
  <v-app dark>
    <v-container>
      <h2 class="display-1 px-4 pb-4">CrunchyGuess</h2>
      <v-layout wrap>
        <v-flex xs12 md7 class="pa-3">
          <guess-list></guess-list>
        </v-flex>
        <v-flex xs12 md5>
          <app-canvas></app-canvas>
        </v-flex>
      </v-layout>
    </v-container>
    <footer class="text-xs-center py-4 grey--text">
      <a href="https://github.com/areebbeigh/crunchyguess">crunchyguess</a>
      by
      <a href="https://github.com/areebbeigh/">@areebbeigh</a>
    </footer>
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
footer a {
  text-decoration: none;
  color: #000;
}
</style>

