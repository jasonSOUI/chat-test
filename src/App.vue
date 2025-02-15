<template>
      <div class="app-container">
        <input
          type="text"
          v-model="searchQuery"
          placeholder="Search for a word..."
          class="search-input"
        />
        <div class="card-container">
          <WordCard
            v-for="(word, index) in filteredWords"
            :key="index"
            :english="word.en_name"
            :chinese="word.ch_name"
          />
        </div>
      </div>
    </template>

    <script>
    import WordCard from './components/WordCard.vue';
    import wordsData from './words.json';

    export default {
      components: {
        WordCard
      },
      data() {
        return {
          searchQuery: '',
          words: wordsData
        };
      },
      computed: {
        filteredWords() {
          if (!this.searchQuery) {
            return this.words;
          }
          return this.words.filter(word =>
            word.en_name.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
            word.ch_name.includes(this.searchQuery)
          );
        }
      }
    };
    </script>

    <style>
    .app-container {
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 16px;
    }

    .search-input {
      width: 300px;
      padding: 12px;
      margin-bottom: 16px;
      border: 1px solid #333;
      border-radius: 4px;
      background-color: #1e1e1e;
      color: #ffffff;
      box-sizing: border-box;
    }

    .card-container {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      padding: 16px;
    }
    </style>
