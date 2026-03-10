<template>
  <div class="word-card">
    <div class="word-section">
      <h2 class="word">{{ word.word }}</h2>
      <button class="audio-btn" @click="$emit('play-audio', word.word)">
        🔊
      </button>
    </div>
    <div class="phonetic" v-if="word.phonetic">
      {{ word.phonetic }}
    </div>
    <div class="meaning">
      {{ word.meaning }}
    </div>
    <div class="progress">
      {{ index + 1 }} / {{ total }}
    </div>
    <div class="buttons">
      <button class="btn" @click="$emit('prev')">上一个</button>
      <button class="btn" @click="$emit('next')">下一个</button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  word: {
    type: Object,
    required: true
  },
  index: {
    type: Number,
    required: true
  },
  total: {
    type: Number,
    required: true
  }
})

defineEmits(['next', 'prev', 'play-audio'])
</script>

<style scoped>
.word-card {
  background: #f5f5f5;
  border-radius: 12px;
  padding: 2rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  margin-bottom: 2rem;
}

.word-section {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 1rem;
}

.word {
  font-size: 2.5rem;
  font-weight: bold;
  color: #333;
  margin: 0;
}

.audio-btn {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  padding: 0.5rem;
  border-radius: 50%;
  transition: background-color 0.3s;
}

.audio-btn:hover {
  background-color: rgba(0, 0, 0, 0.1);
}

.phonetic {
  font-size: 1.2rem;
  color: #666;
  margin-bottom: 1.5rem;
  font-style: italic;
}

.meaning {
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 2rem;
  min-height: 2rem;
}

.progress {
  font-size: 1rem;
  color: #666;
  margin-bottom: 2rem;
}

.buttons {
  display: flex;
  justify-content: center;
  gap: 1rem;
}

.btn {
  padding: 0.8rem 1.5rem;
  border: none;
  border-radius: 6px;
  background-color: #4CAF50;
  color: white;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btn:hover {
  background-color: #45a049;
}

.btn:active {
  transform: scale(0.98);
}
</style>
