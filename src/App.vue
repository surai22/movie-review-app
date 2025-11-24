<script setup>
import { ref } from 'vue'
import MovieList from './components/MovieList.vue'
import MovieForm from './components/MovieForm.vue'

const movies = ref([
  {
    id: 1,
    title: 'インセプション',
    director: 'クリストファー・ノーラン',
    year: 2010,
    genre: 'SF',
    rating: 5,
    review: '夢の中の夢という斬新な設定。映像美と複雑なストーリーが見事に融合した傑作。'
  },
  {
    id: 2,
    title: 'ショーシャンクの空に',
    director: 'フランク・ダラボン',
    year: 1994,
    genre: 'ドラマ',
    rating: 5,
    review: '希望と友情の物語。何度見ても心に響く名作。'
  }
])

const nextId = ref(3)

const addMovie = (movie) => {
  movies.value.push({
    ...movie,
    id: nextId.value++
  })
}

const deleteMovie = (id) => {
  movies.value = movies.value.filter(m => m.id !== id)
}
</script>

<template>
  <div class="app">
    <header>
      <h1>🎬 映画レビューアプリ</h1>
      <p>あなたの映画の感想を記録しましょう</p>
    </header>
    
    <main>
      <MovieForm @add-movie="addMovie" />
      <MovieList :movies="movies" @delete-movie="deleteMovie" />
    </main>
  </div>
</template>

<style scoped>
.app {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}

header {
  text-align: center;
  margin-bottom: 2rem;
  padding: 2rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 12px;
  color: white;
}

header h1 {
  margin: 0 0 0.5rem 0;
  font-size: 2.5rem;
}

header p {
  margin: 0;
  opacity: 0.9;
  font-size: 1.1rem;
}

main {
  display: grid;
  gap: 2rem;
}

@media (max-width: 768px) {
  header h1 {
    font-size: 2rem;
  }
  
  header p {
    font-size: 1rem;
  }
}
</style>
