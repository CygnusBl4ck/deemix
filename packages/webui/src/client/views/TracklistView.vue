<template>
  <div class="tracklist-view">
    <table class="tracklist-table">
      <thead>
        <tr>
          <th class="col-index">#</th>
          <th class="col-cover">Cover</th>
          <th class="col-title">Title</th>
          <th class="col-artist">Artist</th>
          <th class="col-album">Album</th>
          <!-- RELEASE DATE COLUMN HEADER -->
          <th class="col-date">Release Date</th>
          <th class="col-duration">Duration</th>
          <th class="col-actions">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(track, index) in tracks" :key="track.id || index" class="track-row">
          <td class="col-index">{{ index + 1 }}</td>
          <td class="col-cover">
            <img 
              v-if="track.album?.cover_small || track.cover_small" 
              :src="track.album?.cover_small || track.cover_small" 
              alt="Album Cover" 
              class="cover-art"
            />
          </td>
          <td class="col-title">{{ track.title }}</td>
          <td class="col-artist">{{ track.artist?.name || track.artist || 'Unknown Artist' }}</td>
          <td class="col-album">{{ track.album?.title || 'N/A' }}</td>
          <!-- RELEASE DATE DATA CELL -->
          <td class="col-date">{{ track.release_date || track.album?.release_date || 'N/A' }}</td>
          <td class="col-duration">{{ track.duration || 'N/A' }}</td>
          <td class="col-actions">
            <button class="btn-download" @click="$emit('download', track)">Download</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'TracklistView',
  props: {
    tracks: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style scoped>
.tracklist-view {
  width: 100%;
  overflow-x: auto;
  padding: 1rem;
}

.tracklist-table {
  width: 100%;
  border-collapse: collapse;
  text-align: left;
}

.tracklist-table th, 
.tracklist-table td {
  padding: 10px 14px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  vertical-align: middle;
}

.cover-art {
  width: 40px;
  height: 40px;
  border-radius: 4px;
  object-fit: cover;
}

.btn-download {
  padding: 6px 12px;
  border-radius: 4px;
  cursor: pointer;
}
</style>
