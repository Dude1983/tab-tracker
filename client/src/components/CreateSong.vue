<template>
  <v-container fluid>
    <v-layout row wrap>
      <v-flex xs4>
        <panel title="Create Song">
          <v-card-text>
            <v-form>
              <v-text-field label="Title" required :rules="[required]" v-model="song.title"  ></v-text-field>
              <v-text-field label="Album" required :rules="[required]" v-model="song.album" ></v-text-field>
              <v-text-field label="Genre" required :rules="[required]" v-model="song.genre"></v-text-field>
              <v-text-field label="Artist" required :rules="[required]" v-model="song.artist" ></v-text-field>
              <v-text-field label="Album Image" required :rules="[required]" v-model="song.albumImageUrl"></v-text-field>
              <v-text-field label="YouTube ID" type="textarea" required :rules="[required]" v-model="song.youtubeId" ></v-text-field>
            </v-form>
          </v-card-text>
        </panel>
      </v-flex>
      <v-flex xs8>
        <panel title="Song Structure" class="ml-3">
          <v-text-field label="Tab" multi-line required :rules="[required]" v-model="song.tab" ></v-text-field>
          <v-text-field label="Lyrics" multi-line required :rules="[required]" v-model="song.lyrics" ></v-text-field>
        </panel>
        <div class="danger-alert" v-if="error">
          {{ error }}
        </div>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn @click="create" dark color="teal">Create Song</v-btn>
        </v-card-actions>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import Panel from '@/components/Panel'
import SongService from '@/services/SongService'

export default {
  data () {
    return {
      song: {
        title: null,
        album: null,
        genre: null,
        artist: null,
        albumImageUrl: null,
        youtubeId: null,
        lyrics: null,
        tab: null
      },
      error: null,
      required: (value) => !!value || 'Required.'

    }
  },
  components: {
    Panel
  },
  methods: {
    async create () {
      this.error = null
      const areAllFieldsFilledIn = Object
        .keys(this.song)
        .every(key => !!this.song[key])
      if (!areAllFieldsFilledIn) {
        this.error = 'Please fill in all required fields.'
        return
      }
      try {
        await SongService.post(this.song)
        this.$router.push({
          name: 'songs'
        })
      } catch (error) {
        console.log(error)
      }
    }
  }

}
</script>

<style scoped>

</style>
