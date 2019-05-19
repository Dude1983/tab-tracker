<template>
  <v-content>
    <v-container fluid fill-height>
      <v-layout align-center justify-center>
        <v-flex xs12 sm8 md6>
          <panel title="Songs" >
            <div v-for="song in songs"
              :key="song.id">
              {{ song.title }} -
              {{ song.artist }} -
              {{ song.album }}
            </div>
          </panel>
        </v-flex>
      </v-layout>
    </v-container>
  </v-content>
</template>

<script>
import SongService from '@/services/SongService'
import Panel from '@/components/Panel'
export default {
  components: {
    Panel
  },
  data () {
    return {
      songs: null
    }
  },
  async mounted () {
    this.songs = (await SongService.index()).data
  }
}
</script>

<style scoped>

</style>
