<template>
  <div id="app">
    <LightBox :model="model" v-model="currentIndex" />
    <LetterPicker
      v-model="model"
      :letters="letters"
      :currentIndex="currentIndex"
      @new-line="newLine"
    />
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
      if (number !== undefined && number >= 0) {
        this.currentIndex = number;
      } else if (number !== undefined && number === -1){
        //
      } else if (this.currentIndex < 2) {
        this.currentIndex++;
      }
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@300&display=swap");

body {
  margin: 0;
  min-height: 100vh;
  height: 100vh;
  /* background-color: #C4A484; */
}

* {
  box-sizing: border-box;
}

#app {
  min-height: 100%;
  display: grid;
  grid-template-columns: calc(10px * 2 + 8 * 3rem) 1fr;
  align-content: center;
  align-items: center;
  grid-gap: 30px;
  max-width: 1090px;
  margin: auto;
  padding: 0 20px;

  @media only screen and (max-width: 900px){
    grid-template-columns: auto;
    justify-items: center;
    grid-template-rows: auto auto;
    align-items: initial;
    align-content: initial;
    padding: 40px 20px;
  }
}
</style>
