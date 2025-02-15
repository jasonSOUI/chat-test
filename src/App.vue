<template>
      <div class="app-container">
        <input
          type="text"
          v-model="searchQuery"
          placeholder="Search for a word..."
          class="search-input"
        />
        <div class="button-container">
          <button @click="startQuiz">測驗</button>
          <button @click="validateAnswers">驗證</button>
        </div>
        <div class="card-container">
          <WordCard
            v-for="(word, index) in filteredWords"
            :key="index"
            :english="word.en_name"
            :chinese="word.ch_name"
            :isQuizMode="isQuizMode"
            :validate="validate"
            :reset="reset"
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
          words: wordsData,
          isQuizMode: false,
          validate: false,
          reset: false
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
      },
      methods: {
        startQuiz() {
          this.shuffleWords();
          this.isQuizMode = true;
          this.validate = false;
          this.reset = true;
          setTimeout(() => this.reset = false, 0); // Reset the flag immediately after
        },
        validateAnswers() {
          this.validate = true;
        },
        shuffleWords() {
          this.words = this.words
            .map(value => ({ value, sort: Math.random() }))
            .sort((a, b) => a.sort - b.sort)
            .map(({ value }) => value);
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

    .button-container {
      margin-bottom: 16px;
    }

    .button-container button {
      margin: 0 8px;
      padding: 8px 16px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      background-color: #333;
      color: #ffffff;
    }

    .button-container button:hover {
      background-color: #444;
    }

    .card-container {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      padding: 16px;
    }
    </style>
