<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add-movie'])

const form = ref({
  title: '',
  director: '',
  year: new Date().getFullYear(),
  rating: 3,
  review: ''
})

const submitForm = () => {
  if (form.value.title && form.value.director && form.value.review) {
    emit('add-movie', { ...form.value })
    
    // フォームをリセット
    form.value = {
      title: '',
      director: '',
      year: new Date().getFullYear(),
      rating: 3,
      review: ''
    }
  }
}
</script>

<template>
  <div class="movie-form">
    <h2>新しい映画を追加</h2>
    <form @submit.prevent="submitForm">
      <div class="form-group">
        <label for="title">映画タイトル *</label>
        <input
          id="title"
          v-model="form.title"
          type="text"
          placeholder="例: インセプション"
          required
        />
      </div>

      <div class="form-row">
        <div class="form-group">
          <label for="director">監督 *</label>
          <input
            id="director"
            v-model="form.director"
            type="text"
            placeholder="例: クリストファー・ノーラン"
            required
          />
        </div>

        <div class="form-group">
          <label for="year">公開年</label>
          <input
            id="year"
            v-model.number="form.year"
            type="number"
            min="1900"
            :max="new Date().getFullYear() + 5"
          />
        </div>
      </div>

      <div class="form-group">
        <label for="rating">評価: {{ form.rating }} / 5</label>
        <input
          id="rating"
          v-model.number="form.rating"
          type="range"
          min="1"
          max="5"
          step="0.5"
        />
        <div class="rating-display">
          {{ '⭐'.repeat(Math.floor(form.rating)) }}{{ form.rating % 1 !== 0 ? '✨' : '' }}
        </div>
      </div>

      <div class="form-group">
        <label for="review">感想 *</label>
        <textarea
          id="review"
          v-model="form.review"
          placeholder="この映画の感想を書いてください..."
          rows="4"
          required
        ></textarea>
      </div>

      <button type="submit" class="submit-btn">
        ➕ 映画を追加
      </button>
    </form>
  </div>
</template>

<style scoped>
.movie-form {
  background: white;
  padding: 2rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.movie-form h2 {
  margin: 0 0 1.5rem 0;
  color: #333;
  font-size: 1.5rem;
}

form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

label {
  font-weight: 600;
  color: #555;
  font-size: 0.95rem;
}

input[type="text"],
input[type="number"],
textarea {
  padding: 0.75rem;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  font-size: 1rem;
  font-family: inherit;
  transition: border-color 0.2s;
}

input[type="text"]:focus,
input[type="number"]:focus,
textarea:focus {
  outline: none;
  border-color: #667eea;
}

input[type="range"] {
  cursor: pointer;
}

.rating-display {
  font-size: 1.5rem;
  text-align: center;
}

textarea {
  resize: vertical;
  min-height: 100px;
}

.submit-btn {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 1rem 2rem;
  font-size: 1.1rem;
  font-weight: 600;
  border-radius: 8px;
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
}

.submit-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(102, 126, 234, 0.4);
}

.submit-btn:active {
  transform: translateY(0);
}

@media (max-width: 768px) {
  .form-row {
    grid-template-columns: 1fr;
  }
  
  .movie-form {
    padding: 1.5rem;
  }
}
</style>
