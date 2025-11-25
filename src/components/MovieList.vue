<script setup>
import MovieCard from './MovieCard.vue'

defineProps({
  movies: {
    type: Array,
    required: true
  }
})

defineEmits(['delete-movie'])
</script>

<template>
  <div class="movie-list">
    <h2>登録された映画 ({{ movies.length }}件)</h2>
    
    <div v-if="movies.length === 0" class="empty-state">
      <p>📽️ まだ映画が登録されていません</p>
      <p class="subtitle">上のフォームから映画を追加してみましょう！</p>
    </div>
    
    <div v-else class="movies-grid">
      <MovieCard
        v-for="movie in movies"
        :key="movie.id"
        :movie="movie"
        @delete="$emit('delete-movie', movie.id)"
      />
    </div>
  </div>
</template>

<style scoped>
.movie-list {
  background: #2a2a2a;
  padding: 2rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
  border: 1px solid #3a3a3a;
}

.movie-list h2 {
  margin: 0 0 1.5rem 0;
  color: #e0e0e0;
  font-size: 1.5rem;
}

.empty-state {
  text-align: center;
  padding: 3rem 1rem;
  color: #888;
}

.empty-state p {
  margin: 0.5rem 0;
  font-size: 1.2rem;
}

.empty-state .subtitle {
  font-size: 1rem;
  color: #666;
}

.movies-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.5rem;
}

@media (max-width: 768px) {
  .movie-list {
    padding: 1.5rem;
  }
  
  .movies-grid {
    grid-template-columns: 1fr;
  }
}
</style>
