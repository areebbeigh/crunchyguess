<template>
  <div>
    <div class="search-area">
      <v-text-field
        class="search-input"
        v-model="query"
        label="Search (Kitsu)"
        outline
      ></v-text-field>
      <v-list v-if="fetchedAnimu.length" class="search-results pa-2 mb-4">
        <v-subheader class="grey--text">
          Search results - 2018
        </v-subheader>
        <div :key="anime.id" v-for="anime in fetchedAnimu" class="mb-2">
          <v-list-tile
            avatar
            @click=""
          >
            <v-list-tile-avatar tile>
              <img :src="anime.posterImage.tiny">
            </v-list-tile-avatar>

            <v-list-tile-content>
              <v-list-tile-title>{{ anime.canonicalTitle }}</v-list-tile-title>
            </v-list-tile-content>

            <v-list-tile-action v-if="selectedAnimu.length < 6">
              <v-btn flat icon color="green" @click="addToList(anime)">
                <v-icon>add</v-icon>
              </v-btn>
            </v-list-tile-action>
          </v-list-tile>
        </div>
      </v-list>
    </div>

    <v-list v-if="this.selectedAnimu.length" class="pa-2">
      <v-subheader class="grey--text">
        Your predictions
      </v-subheader>
      <v-layout wrap>
        <v-flex 
          xs12
          class="mb-2"
          :key="anime.id" 
          v-for="anime in selectedAnimu">
            <v-list-tile
              avatar
              @click=""
            >
              <v-list-tile-avatar tile>
                <img :src="anime.posterImage.tiny">
              </v-list-tile-avatar>

              <v-list-tile-content>
                <v-list-tile-title>{{ anime.canonicalTitle }}</v-list-tile-title>
              </v-list-tile-content>

              <v-list-tile-action>
                <v-btn flat icon color="red" @click="removeFromList(anime)">
                  <v-icon>close</v-icon>
                </v-btn>
              </v-list-tile-action>
            </v-list-tile>
          </v-flex>
      </v-layout>
    </v-list>
    <v-btn class="ma-0 mt-4" style="width:100%" flat @click="$root.$emit('generate', selectedAnimu)">generate poster</v-btn>
  </div>
</template>

<script>
import Kitsu from 'kitsu'
import { debounce } from 'lodash'

export default {
  data () {
    return {
      guesses: [],
      query: null,
      fetchedAnimu: [], // return list of anime
      selectedAnimu: [], // predictions
      api: new Kitsu()
    }
  },

  methods: {
    addToList (anime) {
      if (this.selectedAnimu.length < 6 && !this.selectedAnimu.includes(anime)) {
        this.selectedAnimu.push(anime)
        this.fetchedAnimu.splice(this.fetchedAnimu.indexOf(anime), 1)
      }
    },

    removeFromList (anime) {
      this.fetchedAnimu.push(anime)
      this.selectedAnimu.splice(this.selectedAnimu.indexOf(anime), 1)
    }
  },

  watch: {
    query: {
      handler: debounce(async function (value) {
        try {
          const response = await this.api.get('anime',  { 
            filter: { seasonYear: 2018, text: value }, 
            page: { limit: 20 } 
          })
  
          this.fetchedAnimu = response.data
        } catch (err) {
          console.error(err)
        }
      }, 700)
    }
  }
}
</script>

<style scoped>
.search-results {
  height: 250px;
  overflow-y: scroll;
}
</style>
