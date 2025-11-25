<script setup>
defineProps({
  movie: {
    type: Object,
    required: true
  }
})

defineEmits(['delete'])
</script>

<template>
  <div class="movie-card">
    <div class="movie-header">
      <h3>{{ movie.title }}</h3>
      <button class="delete-btn" @click="$emit('delete')" title="削除">
        🗑️
      </button>
    </div>
    
    <div class="movie-info">
      <p class="director">🎬 {{ movie.director }}</p>
      <p class="year">📅 {{ movie.year }}年</p>
      <p class="genre">🎭 {{ movie.genre }}</p>
    </div>
    
    <div class="rating">
      <span class="stars">{{ '⭐'.repeat(Math.floor(movie.rating)) }}{{ movie.rating % 1 !== 0 ? '✨' : '' }}</span>
      <span class="rating-number">{{ movie.rating }} / 5</span>
    </div>
    
    <div class="review">
      <p>{{ movie.review }}</p>
    </div>
  </div>
</template>

<style scoped>
.movie-card {
  background: linear-gradient(135deg, #2d3748 0%, #1a202c 100%);
  padding: 1.5rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.4);
  transition: transform 0.2s, box-shadow 0.2s;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  border: 1px solid #3a3a3a;
}

.movie-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.6);
  border-color: #4a4a4a;
}

.movie-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 1rem;
}

.movie-header h3 {
  margin: 0;
  color: #e0e0e0;
  font-size: 1.3rem;
  flex: 1;
  word-break: break-word;
}

.delete-btn {
  background: rgba(50, 50, 50, 0.8);
  border: none;
  padding: 0.5rem;
  border-radius: 6px;
  cursor: pointer;
  font-size: 1.2rem;
  transition: background-color 0.2s, transform 0.2s;
  flex-shrink: 0;
}

.delete-btn:hover {
  background: rgba(200, 50, 50, 0.8);
  transform: scale(1.1);
}

.movie-info {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.movie-info p {
  margin: 0;
  color: #b0b0b0;
  font-size: 0.95rem;
}

.director {
  font-weight: 600;
}

.rating {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem;
  background: rgba(50, 50, 50, 0.6);
  border-radius: 8px;
}

.stars {
  font-size: 1.2rem;
}

.rating-number {
  font-weight: 600;
  color: #7c8aff;
}

.review {
  background: rgba(40, 40, 40, 0.8);
  padding: 1rem;
  border-radius: 8px;
  border-left: 4px solid #7c8aff;
}

.review p {
  margin: 0;
  color: #d0d0d0;
  line-height: 1.6;
  font-size: 0.95rem;
}
</style>
