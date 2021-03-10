<template>
  <div>
    <h1 class="is-1 title">{{ content }}</h1>
    <h2 class="is-3 subtitle" v-if="!completed && started">Word {{ current + 1 }} / {{ words.length }}</h2>
    <b-button @click="speak" v-if="!completed && !started">Start</b-button>
    <b-button @click="speak" v-if="started && !completed">Repeat Word</b-button>
    <b-input
      class="word-input"
      v-model="wordInput"
      placeholder="Spell word here."
      v-on:keydown.native.enter="submitWord"
      v-if="!completed && started"
      autofocus
    >
    </b-input>
    <h2 class="is-2 subtitle" v-if="completed">
      Your score was {{ correct }}/{{ words.length }}
    </h2>
    <b-button @click="restart" v-if="completed">Restart</b-button>
    <div v-if="completed" class="columns is-centered">
      <div class="column is-one-fifth header">Word Given</div>
      <div class="column is-one-fifth header">Word Spelled</div>
    </div>
    <div v-if="completed">
      <div class="columns is-centered" v-for="word ,index in words" :key="index + 1">
        <div class="column is-one-fifth word-given">{{ word.word }}</div>
        <div class="column is-one-fifth word-spelled">{{ word.userInput.charAt(0).toUpperCase() + word.userInput.slice(1) }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import { spellingWords } from "./wordData";
export default {
  data() {
    return {
      words: [...spellingWords],
      correct: 0,
      current: 0,
      wordInput: "",
      content: "Spelling Test",
      completed: false,
      started: false
    };
  },
  methods: {
    speak() {
      const word = new SpeechSynthesisUtterance(this.words[this.current].word);
      speechSynthesis.speak(word);
      if (this.started === true) {
        return;
      }
      this.started = true;
    },
    checkScore() {
      for (const x in this.words) {
        if (
          this.words[x].word.toLowerCase() ===
          this.words[x].userInput.toLowerCase()
        ) {
          this.correct += 1;
        }
      }
    },
    submitWord() {
      if(!this.started){
        this.started = true
        this.speak()
        return
      }
      this.words[this.current].userInput = this.wordInput;
      this.wordInput = "";
      this.current += 1;
      if (this.current === this.words.length) {
        this.content = "Congratulations. You Won!";
        this.completed = true;
        this.checkScore();
        return;
      }
      this.speak();
    },
    restart() {
      this.current = 0;
      this.completed = false;
      this.content = "Spelling Test";
      this.started = false;
    }
  }
};
</script>

<style>
.spelling-check{
  display: flex;
  margin-left: 40%;
  margin-right: 40%;
  justify-content: space-around;
}

.spelling-check:last-child{
  margin-left: 40
}

.word-given{
  border-right: 1px solid black;
}

.word-spelled{
  border-left: 1px solid black;
}

.header{
  margin-top: 2.5em;
  font-weight: bolder;
  border-bottom: 2px solid black;
}

.word-input{
  margin-left: 43%;
  margin-right: 43%;
  margin-top: 1em;
}
</style>
