<template>
  <div class="letter-picker">
    <div class="letter-picker__table" v-if="!keyboardLayout">
      <button
        class="card"
        v-for="(count, letter) in letters"
        :key="letter"
        @click="letterClicked(letter)"
        :disabled="checkCount(letter) && limitedLetter"
      >
        {{ letter }}
      </button>
      <button
        class="card"
        @click="letterClicked(' ')"
      >&nbsp;</button>
    </div>
    <div class="letter-picker__table letter-picker__table--keyboard" v-else>
      <button
        class="card"
        v-for="key in keyboard"
        :key="'keyboard' + key"
        @click="letterClicked(key)"
        :disabled="checkCount(key) && limitedLetter"
      >
        {{ key }}
      </button>
    </div>
    <div class="letter-picker__tool">
      <button @click="newLine">
        Next Row
        <span class="key">Enter</span>
      </button>
      <button @click="backspace">
        Backspace
        <span class="key">Backspace</span>
      </button>
      <button @click="deleteRow">
        Delete Row
        <span class="key">Delete</span>
      </button>
      <button @click="reset">
        Reset
        <span class="key">Esc</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "LetterPicker",
  props: ["letters", "currentIndex", "limitedLetter", 'keyboardLayout'],
  data() {
    return {
      localModel: ["", "", ""],
      keyboard: ["!","@","&","#","?","'","€","£","♫","1","2","3","4","5","6","7","8","9","0","Q","W","E","R","T","Y","U","I","O","P","A","S","D","F","G","H","J","K","L","Z","X","C","V","B","N","M","🙂","😝","😂","👍"," ","♥️","🎈","🍾","😎","😍"]
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
      console.log(e.key)
      e.preventDefault();
      var key = e.key;
      if (/Enter/.test(key)){
        this.newLine();
      } else if (/\s/.test(key)) {
        this.letterClicked(' ')
      } else if (/Backspace/.test(key)) {
        this.backspace();
      } else if (/Delete/.test(key)) {
        this.deleteRow();
      } else if (/Escape/.test(key)) {
        this.reset();
      } else if (/ArrowDown/.test(key)) {
        this.newLine();
      } else if (/ArrowUp/.test(key)) {
        this.newLine(this.currentIndex - 1);
      } else if (/^\w\b/.test(key)) {
        key = key.toUpperCase();
        if ( !this.checkCount(key) || !this.limitedLetter ){
          this.letterClicked(key)
        }
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
        this.$set(
          this.localModel,
          this.currentIndex,
          this.localModel[this.currentIndex] + letter
        );
      } else {
        console.error("max length!");
      }
    },
    newLine(number) {
      this.$emit("new-line", number);
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
<style lang="scss">
.card {
  background: #fff;
  color: #000;
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

  &:hover {
    background-color: #ddd;
  }
}

.key {
  font-size: 0.7em;
  margin-top: .7em;
  border: 1px solid #000;
  padding: .15em .5em;
  border-radius: 3px;
  background-color: #ccc;
  transition: .5s;
}
</style>

<style lang="scss" scoped>
.letter-picker {
  &__table {

    &--keyboard {
      display: grid;
      grid-template-columns: repeat(10, 3rem);
      grid-template-rows: 5rem;
      grid-gap: 0.5rem;
      justify-content: center;

      .card {
        margin: 0;

        &:nth-child(-n+9){
          margin-left: 1.5rem;
        }

        &:nth-child(n+10){
          grid-row-start: 2;
        }

        &:nth-child(n+20){
          grid-row-start: 3;
        }

        &:nth-child(n+30){
          grid-row-start: 4;
          margin-left: 1.5rem;
        }

        &:nth-child(n+39){
          margin-left: 4.5rem;
          grid-row-start: 5;
        }

        &:nth-child(n+46){
          grid-row-start: 6;
          margin-left: 0;
        }
      }
    }
  }

  &__tool {
    margin-top: 30px;
    display: grid;
    grid-template-columns: repeat(4, minmax(0, 1fr));
    grid-gap: 10px;

    button {
      border: none;
      color: #000;
      height: 60px;

      display: inline-flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      transition: .3s;
      background-color: #eee;
      cursor: pointer;

      &:hover {
        background-color: #ddd;
      }
    }
  }
}
</style>
