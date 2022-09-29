<template>
  <div id="app">
    <LightBox :model="model" v-model="currentIndex" />
    <LetterPicker
      v-model="model"
      :letters="letters"
      :currentIndex="currentIndex"
      @new-line="newLine"
    />

    Results: {{ model }} current: {{ currentIndex }} length:
    {{ model[currentIndex].length }}
  </div>
</template>

<script>
import LetterPicker from "@/components/LetterPicker";
import LightBox from "@/components/LightBox";

export default {
  name: "App",
  components: {
    LetterPicker,
    LightBox,
  },
  data() {
    return {
      model: ["", "", ""],
      currentIndex: 0,
      letters: {
        A: 4,
        B: 2,
        C: 2,
        D: 3,
        E: 4,
        F: 2,
        G: 2,
        H: 3,
        I: 3,
        J: 2,
        K: 2,
        L: 2,
        M: 2,
        N: 3,
        O: 3,
        P: 3,
        Q: 1,
        R: 3,
        S: 2,
        T: 3,
        U: 3,
        V: 2,
        W: 2,
        X: 1,
        Y: 2,
        Z: 1,
        0: 1,
        1: 2,
        2: 2,
        3: 1,
        4: 1,
        5: 1,
        6: 1,
        7: 1,
        8: 1,
        9: 1,
        "@": 1,
        "&": 1,
        "#": 1,
        "?": 1,
        "!": 1,
        "'": 1,
        "€": 1,
        "£": 1,
        "♫": 1,
        "🙂": 1,
        "😝": 1,
        "😂": 1,
        "👍": 1,
        "♥️": 1,
        "🎈": 1,
        "🍾": 1,
        "😎": 1,
        "😍": 1,
      },
    };
  },
  methods: {
    newLine(number) {
      console.log(number);
      if (number !== undefined) {
        this.currentIndex = number;
      } else if (this.currentIndex < 2) {
        this.currentIndex++;
      }
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@300&display=swap");

#app {
  display: grid;
  grid-template-columns: calc(10px * 2 + 8 * 3rem) 1fr;
}
</style>
