<template>
  <v-layout>
    <v-flex xs4>
      <panel title="Song metadata">
        <v-text-field
          label="Title"
          required
          :rules="[required]"
          v-model="song.title"
        ></v-text-field>
        <v-text-field
          label="Artist"
          required
          :rules="[required]"
          v-model="song.artist"                  
          required
        ></v-text-field>
        <v-text-field
          label="Genre"
          required
          :rules="[required]"
          v-model="song.genre"                  
          required
        ></v-text-field>
        <v-text-field
          label="Album"
          required
          :rules="[required]"
          v-model="song.album"                  
        ></v-text-field>
        <v-text-field
          label="AlbumImage"
          required
          :rules="[required]"
          v-model="song.albumImage"                  
        ></v-text-field>
        <v-text-field
          label="Youtube Video"
          v-model="song.youtubeId"                  
        ></v-text-field>      
      </panel>
    </v-flex>
    <v-flex xs8>
      <panel title="Song structure" class="ml-4">
        <v-text-field
          label="Lyrics"
          multi-line
          required
          :rules="[required]"
          v-model="song.lyrics"                  
        ></v-text-field>
        <v-text-field
          label="Tabs"
          multi-line
          required
          :rules="[required]"
          v-model="song.tab"                  
        ></v-text-field>
      </panel>
      <div class="danger-alert" v-if="error">
        {{error}}
      </div>
      <v-btn
        dark
        class="cyan"
        @click="create">
        Create Song
      </v-btn>  
    </v-flex>  
  </v-layout>
</template>

<script>
import Panel from '@/components/Panel'
import SongsService from '@/services/SongsService'

export default {
  data () {
    return {
      song: {
        title: null,
        artist: null,
        genre: null,
        album: null,
        albumImage: null,
        youtubeId: null,
        lyrics: null,
        tab: null
      },
      error: null,
      required: (value) => !!value || 'Required'
    }
  },
  methods: {
    async create () {
      // Call API
      this.error = null
      const areAllFieldsFilledIn = Object
        .keys(this.song)
        .every(key => !!this.song[key])

      if (!areAllFieldsFilledIn) {
        this.error = 'Please fill all the required fills'
        return
      }
      try {
        await SongsService.post(this.song)
        this.$router.push({name: 'songs'})
      } catch (err) {
        console.log(err)
      }
    }
  },
  components: {
    Panel
  }
}
</script>

<style scoped>

</style>
