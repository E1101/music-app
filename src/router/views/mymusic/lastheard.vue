<template>
<main class="main-container" :class="{ 'stage-compact': $route.meta.header === 'compact' }">

  <!--Stage-->
  <stage
  type="My Music"
  title="Last heard"
  :image="lastheard[0].track.album.images[0].url"
  ></stage>

  <div class="page-container">

    <section class="page-section lastheard">
      <ol class="flex-table">
        <flextable
        v-for="(lastheard, index) in lastheard"
        :key="lastheard.track.id"
        :type="lastheard.track.type"
        :image="lastheard.track.album.images[0].url"
        :title="lastheard.track.name"
        :artist="lastheard.track.artists[0].name"
        :artistID="lastheard.track.artists[0].id"
        :album="lastheard.track.album.name"
        :albumID="lastheard.track.album.id"
        :duration="lastheard.track.duration_ms"
        :index="index"
        ></flextable>
      </ol>
    </section>

  </div>

</main>
</template>
<script>
import spotifyApi from '../../../api/'

export default {
  data() {
    return {
      lastheard: {}
    }
  },
  created() {
    // fetch the data when the view is created and the data is
    // already being observed
    this.fetchData()
  },
  watch: {
    // call again the method if the route changes
    '$route': 'fetchData'
  },
  methods: {
    fetchData() {
      // Get this playlist's tracks
      spotifyApi.getMyRecentlyPlayedTracks()
        .then(response => this.lastheard = response.items)
    }
  }
}
</script>
