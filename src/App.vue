<template>
  <div class="app">
    <h1>雅思单词学习</h1>
    <WordCard 
      :word="currentWord" 
      :index="currentIndex" 
      :total="wordList.length"
      @next="nextWord"
      @prev="prevWord"
      @play-audio="playAudio"
    />
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import WordCard from './components/WordCard.vue'
import ieltsData from './data/IETLS1.json'
import { getPhonetic } from './utils/phonetic-utils.js'

const wordList = ref([])
const currentIndex = ref(0)

const currentWord = computed(() => {
  if (wordList.value.length === 0) return { word: '', meaning: '', phonetic: '' }
  const entry = wordList.value[currentIndex.value]
  return { word: entry.word, meaning: entry.meaning, phonetic: entry.phonetic || '' }
})

const prevWord = () => {
  if (currentIndex.value > 0) currentIndex.value--
  else currentIndex.value = wordList.value.length - 1
}

const nextWord = () => {
  if (currentIndex.value < wordList.value.length - 1) currentIndex.value++
  else currentIndex.value = 0
}

const playAudio = (word) => {
  if (!word) return
  
  const u = new SpeechSynthesisUtterance(word)
  window.speechSynthesis.cancel()
  window.speechSynthesis.speak(u)
}

onMounted(() => {
  const wordsWithPhonetic = []
  
  // 遍历所有类别
  for (const category in ieltsData) {
    const words = ieltsData[category]
    for (const wordObj of words) {
      for (const [word, meaning] of Object.entries(wordObj)) {
        const phonetic = getPhonetic(word)
        wordsWithPhonetic.push({ word, meaning, phonetic })
      }
    }
  }
  
  wordList.value = wordsWithPhonetic
})
</script>

<style scoped>
.app {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
  font-family: Arial, sans-serif;
  text-align: center;
}
h1 {
  color: #333;
  margin-bottom: 2rem;
}
</style>
