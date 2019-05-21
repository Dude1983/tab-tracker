<template>
  <div>

  </div>
</template>

<script>
import SongService from '@/services/SongService'
export default {
  data () {
    return {
      song: null
    }
  },
  async mounted () {
    const songId = this.$store.state.route.params.songId
    console.log(songId)
    this.song = (await SongService.show(songId)).data
  }
}
</script>

<style scoped>

</style>
