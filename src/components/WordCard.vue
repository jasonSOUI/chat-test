<template>
      <div :class="['card', { 'incorrect': isIncorrect }]">
        <div v-if="isQuizMode">
          <input v-model="userEnglish" placeholder="Enter English" />
          <input v-model="userChinese" placeholder="Enter Chinese" />
          <div v-if="validate" class="correct-answers">
            <p>{{ english }}</p>
            <p>{{ chinese }}</p>
          </div>
        </div>
        <div v-else>
          <h3>{{ english }}</h3>
          <p>{{ chinese }}</p>
        </div>
        <button @click="playPronunciation">發音</button>
      </div>
    </template>

    <script>
    export default {
      props: {
        english: String,
        chinese: String,
        isQuizMode: Boolean,
        validate: Boolean,
        reset: Boolean
      },
      data() {
        return {
          userEnglish: '',
          userChinese: ''
        };
      },
      watch: {
        reset(newVal) {
          if (newVal) {
            this.userEnglish = '';
            this.userChinese = '';
          }
        }
      },
      computed: {
        isIncorrect() {
          if (!this.validate) return false;
          return this.userEnglish.toLowerCase() !== this.english.toLowerCase() ||
                 this.userChinese !== this.chinese;
        }
      },
      methods: {
        playPronunciation() {
          const utterance = new SpeechSynthesisUtterance(this.english);
          utterance.lang = 'en-US';
          speechSynthesis.speak(utterance);
        }
      }
    };
    </script>

    <style>
    .card {
      border: 1px solid #333;
      padding: 16px;
      border-radius: 8px;
      width: 200px;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
      box-sizing: border-box;
      background-color: #1e1e1e;
      color: #ffffff;
      margin: 8px;
    }

    .card.incorrect {
      border-color: red;
    }

    .card input {
      width: calc(100% - 16px);
      margin-bottom: 8px;
      padding: 8px;
      border: 1px solid #333;
      border-radius: 4px;
      background-color: #2e2e2e;
      color: #ffffff;
      box-sizing: border-box;
    }

    .card button {
      background-color: #333;
      color: #ffffff;
      border: none;
      padding: 8px 16px;
      border-radius: 4px;
      cursor: pointer;
    }

    .card button:hover {
      background-color: #444;
    }

    .correct-answers {
      margin-top: 8px;
      color: #00ff00;
    }
    </style>
