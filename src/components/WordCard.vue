<template>
      <div class="card">
        <h3>{{ english }}</h3>
        <p>{{ chinese }}</p>
        <button @click="playPronunciation">發音</button>
      </div>
    </template>

    <script>
    export default {
      props: {
        english: String,
        chinese: String
      },
      methods: {
        playPronunciation() {
          const utterance = new SpeechSynthesisUtterance(this.english);
          utterance.lang = 'en-US'; // 設定語言為美式英語
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
    </style>
