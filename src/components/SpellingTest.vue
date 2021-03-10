<template>
  <div>
    <h1 class="is-1 title">{{ content }}</h1>
    <b-button @click="speak" v-if="!completed && !started">Start</b-button>
    <b-button @click="speak" v-if="started && !completed">Repeat Word</b-button>
    <b-field label="Word Input" v-if="!completed">
      <b-input
        v-model="wordInput"
        placeholder="Spell word here."
        v-on:keydown.native.enter="submitWord"
      >
      </b-input>
    </b-field>
    <h2 class="is-2 subtitle" v-if="completed">
      Your score was {{ correct }}/{{ words.length }}
    </h2>
    <b-button @click="restart" v-if="completed">Restart</b-button>
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

<style></style>
