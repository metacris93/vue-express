<template>
  <v-layout row>
    <v-flex xs6 offset-xs3>
      <panel title="Songs">
        <div slot="action">
          <router-link :to="{name: 'songs-create'}" slot="action">
            <v-btn 
              class="cyan"
              medium
              @click="navigateTo({name: 'songs-create'})"
              absolute
              right
              middle
              fab>
              <v-icon>add</v-icon>
            </v-btn>
          </router-link>
        </div>
        <div class="song" v-for="song in songs" :key="song.title">
          <v-layout>
            <v-flex xs6>
              <div class="song-title">
                {{song.title}}
              </div>

              <div class="song-title">
                {{song.artist}}
              </div>

              <div class="song-title">
                {{song.genre}}
              </div>
              <v-btn
                dark
                class="cyan"
                @click="navigateTo({name: 'song', params: {songId: song.id}})">
                View
              </v-btn>  
            </v-flex>
            <v-flex xs6>
              <img class="album-image" :src="song.albumImage">
            </v-flex>
          </v-layout>  
        </div>
      </panel>  
    </v-flex>
  </v-layout>    
</template>

<script>
import Panel from '@/components/Panel'
import SongsService from '@/services/SongsService'
export default {
  components: {
    Panel
  },
  data () {
    return {
      songs: null
    }
  },
  methods: {
    navigateTo (router) {
      this.$router.push(router)
    }
  },
  async mounted () {
    // do a request to the backend for all the songs
    this.songs = (await SongsService.index()).data
  }
}
</script>

<style scoped>
  .song {
    padding: 20px;
    height: 330px;
    overflow: hidden;
  }
  .album-image {
    width: 70%;
    margin: 0 auto;
  }
</style>
