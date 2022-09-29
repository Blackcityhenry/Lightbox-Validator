<template>
  <div class="letter-picker">
    <div class="letter-picker__table">
      <button
        class="card"
        v-for="(count, letter) in letters"
        :key="letter"
        @click="letterClicked(letter)"
        :disabled="checkCount(letter)"
      >
        {{ letter }}
      </button>
      <button
        class="card"
        @click="letterClicked(' ')"
      >&nbsp;</button>
    </div>
    <div class="letter-picker__tool">
      <button @click="newLine">Next Row</button>
      <button @click="backspace">Backspace</button>
      <button @click="deleteRow">Delete Row</button>
      <button @click="reset">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "LetterPicker",
  props: ["letters", "currentIndex"],
  data() {
    return {
      localModel: ["", "", ""],
    };
  },
  computed: {
    letterUsed() {
      var string = this.localModel.join("");

      return string.split("").reduce((total, letter) => {
        total[letter] ? total[letter]++ : (total[letter] = 1);
        return total;
      }, {});
    },
  },
  watch: {
    localModel: {
      handler(array) {
        this.$emit("input", array);
      },
      deep: true,
    },
  },
  methods: {
    letterListener(e){
      console.log(e)
      var key = e.key;
      if (/Enter/.test(key)){
        this.newLine();
      } else if (/\s/.test(key)) {
        this.letterClicked(' ')
      } else if (/Backspace/.test(key)) {
        this.backspace();
      } else if (/\w/.test(key)) {
        key = key.toUpperCase();
        this.letterClicked(key)
      }
    },
    letterClicked(letter) {
      if (
        this.localModel[this.currentIndex].length === 8 &&
        this.currentIndex < 2
      ) {
        this.newLine();

        this.$nextTick(() => {
          if (this.localModel[this.currentIndex].length === 8) {
            this.newLine();
          }

          this.$set(
            this.localModel,
            this.currentIndex,
            this.localModel[this.currentIndex] + letter
          );
        });
      } else if (this.localModel[this.currentIndex].length < 8) {
        console.log("simple add");
        this.$set(
          this.localModel,
          this.currentIndex,
          this.localModel[this.currentIndex] + letter
        );
      } else {
        console.error("max length!");
      }
    },
    newLine() {
      this.$emit("new-line");
    },
    backspace() {
      this.$set(
        this.localModel,
        this.currentIndex,
        this.localModel[this.currentIndex].slice(0, -1)
      );
    },
    deleteRow() {
      this.$set(this.localModel, this.currentIndex, "");
    },
    reset() {
      this.localModel = ["", "", ""];
      this.$emit("new-line", 0);
    },
    checkCount(letter) {
      var limit = this.letters[letter];
      var used = this.letterUsed[letter];
      return used >= limit;
    },
  },
  mounted(){
    window.addEventListener('keyup', this.letterListener)
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.card {
  background: #fff;
  border: 1px solid #ccc;
  width: 3rem;
  height: 5rem;
  margin: 0.25rem;

  font-size: 2.75rem;
  font-family: "Barlow Condensed", monospace;

  display: inline-flex;
  justify-content: center;
  align-items: center;
  padding: 0;
  transition: .3s;
  cursor: pointer;

  &[disabled] {
    opacity: 0.3;
  }
}

.letter-picker {
  &__table {
  }

  &__tool {
    margin-top: 30px;
    display: grid;
    grid-template-columns: repeat(4, minmax(0, 1fr));
    grid-gap: 10px;

    button {
      border: none;

      height: 40px;

      display: inline-flex;
      justify-content: center;
      align-items: center;
    }
  }
}
</style>
