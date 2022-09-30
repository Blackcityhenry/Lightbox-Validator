<template>
    <div class="page-setting">
      <div class="page-setting__btn">
        <button @click="toggleBoxOpen">
            <svg id="Layer_1" style="enable-background:new 0 0 512 512;" version="1.1" xml:space="preserve" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="63.98 64 383.63 384.13"><path d="M424.5,216.5h-15.2c-12.4,0-22.8-10.7-22.8-23.4c0-6.4,2.7-12.2,7.5-16.5l9.8-9.6c9.7-9.6,9.7-25.3,0-34.9l-22.3-22.1  c-4.4-4.4-10.9-7-17.5-7c-6.6,0-13,2.6-17.5,7l-9.4,9.4c-4.5,5-10.5,7.7-17,7.7c-12.8,0-23.5-10.4-23.5-22.7V89.1  c0-13.5-10.9-25.1-24.5-25.1h-30.4c-13.6,0-24.4,11.5-24.4,25.1v15.2c0,12.3-10.7,22.7-23.5,22.7c-6.4,0-12.3-2.7-16.6-7.4l-9.7-9.6  c-4.4-4.5-10.9-7-17.5-7s-13,2.6-17.5,7L110,132c-9.6,9.6-9.6,25.3,0,34.8l9.4,9.4c5,4.5,7.8,10.5,7.8,16.9  c0,12.8-10.4,23.4-22.8,23.4H89.2c-13.7,0-25.2,10.7-25.2,24.3V256v15.2c0,13.5,11.5,24.3,25.2,24.3h15.2  c12.4,0,22.8,10.7,22.8,23.4c0,6.4-2.8,12.4-7.8,16.9l-9.4,9.3c-9.6,9.6-9.6,25.3,0,34.8l22.3,22.2c4.4,4.5,10.9,7,17.5,7  c6.6,0,13-2.6,17.5-7l9.7-9.6c4.2-4.7,10.2-7.4,16.6-7.4c12.8,0,23.5,10.4,23.5,22.7v15.2c0,13.5,10.8,25.1,24.5,25.1h30.4  c13.6,0,24.4-11.5,24.4-25.1v-15.2c0-12.3,10.7-22.7,23.5-22.7c6.4,0,12.4,2.8,17,7.7l9.4,9.4c4.5,4.4,10.9,7,17.5,7  c6.6,0,13-2.6,17.5-7l22.3-22.2c9.6-9.6,9.6-25.3,0-34.9l-9.8-9.6c-4.8-4.3-7.5-10.2-7.5-16.5c0-12.8,10.4-23.4,22.8-23.4h15.2  c13.6,0,23.3-10.7,23.3-24.3V256v-15.2C447.8,227.2,438.1,216.5,424.5,216.5z M336.8,256L336.8,256c0,44.1-35.7,80-80,80  c-44.3,0-80-35.9-80-80l0,0l0,0c0-44.1,35.7-80,80-80C301.1,176,336.8,211.9,336.8,256L336.8,256z"></path></svg>
        </button>
      </div>
      <div class="page-setting__box" v-if="boxOpen">

        <div class="page-setting__title">
          <span class="card">S</span>
          <span class="card">E</span>
          <span class="card">T</span>
          <span class="card">T</span>
          <span class="card">I</span>
          <span class="card">N</span>
          <span class="card">G</span>
        </div>

        <div class="page-setting__section">
          <button @click="setData('darkMode', false)">
            <div class="card" :class="isActive(darkMode, false)">
              🌞
            </div>
          </button>
          <button @click="setData('darkMode', true)">
            <div class="card" :class="isActive(darkMode, true)">
              🌚
            </div>
          </button>
        </div>

        <div class="page-setting__section">
          <label>
            <input type="radio" v-model="fontWeight" value="300" hidden>
            <span class="card" style="font-weight: 300" :class="isActive(fontWeight ,'300')">A</span>
          </label>
          <label>
            <input type="radio" v-model="fontWeight" value="400" hidden>
            <span class="card" style="font-weight: 400" :class="isActive(fontWeight ,'400')">A</span>
          </label>
          <label>
            <input type="radio" v-model="fontWeight" value="500" hidden>
            <span class="card" style="font-weight: 500" :class="isActive(fontWeight ,'500')">A</span>
          </label>
        </div>

        <div class="page-setting__section">
          <button @click="setData('limitedLetter', true)">
            <div class="card" :class="isActive(limitedLetter, true)">
              🔒
            </div>
          </button>
          <button @click="setData('limitedLetter', false)">
            <div class="card" :class="isActive(limitedLetter, false)">
              🔓
            </div>
          </button>
        </div>

        <div class="page-setting__section">
          <button @click="setData('keyboardLayout', false)">
            <div class="card" :class="isActive(keyboardLayout, false)">
              🔠
            </div>
          </button>
          <button @click="setData('keyboardLayout', true)">
            <div class="card" :class="isActive(keyboardLayout, true)">
              ⌨️
            </div>
          </button>
        </div>
      </div>
    </div>
  </template>

  <script>
  export default {
    name: 'PageSetting',
    data(){
      return ({
        darkMode: false,
        fontWeight: '300',
        limitedLetter: true,
        keyboardLayout: false,
        boxOpen: false,
      })
    },
    watch: {
      darkMode(boolean){
        if ( boolean ){
          document.body.classList.add('dark-mode')
        } else {
          document.body.classList.remove('dark-mode')
        }
      },
      fontWeight(fw){
        document.body.classList.remove('fw-300')
        document.body.classList.remove('fw-400')
        document.body.classList.remove('fw-500')
        document.body.classList.add('fw-'+fw)
      },
      limitedLetter(boolean){
        this.$emit('property-updated', 'limitedLetter', boolean)
      },
      keyboardLayout(boolean){
        this.$emit('property-updated', 'keyboardLayout', boolean)
      }
    },
    methods: {
      toggleBoxOpen(){
          this.boxOpen = !this.boxOpen;
        },
      setData(property, boolean){
        this[property] = boolean;
      },
      isActive(compare1, compare2){
        return compare1 === compare2 && 'active';
      }
    },
    mounted(){
      this.darkMode = window.matchMedia("(prefers-color-scheme: dark)").matches;

      document.body.classList.add('fw-300')
    }
  }
  </script>

  <style lang="scss">
  body {
    transition: background-color .5s;
  }
  .dark-mode {
    background-color: #444;

    .key {
      background-color: #000;
      color: #fff;
    }

    .page-setting__box {
      background-color: #444;
    }
  }

  .fw-300 {
    .card {
      font-weight: 300;
    }

    .light-box {
      > div {
        font-weight: 300;
      }
    }
  }
  .fw-400 {
    .card {
      font-weight: 400;
    }

    .light-box {
      > div {
        font-weight: 400;
      }
    }
  }
  .fw-500 {
    .card {
      font-weight: 500;
    }

    .light-box {
      > div {
        font-weight: 500;
      }
    }
  }

  </style>

  <style lang="scss">
  .page-setting {
    position: fixed;
    top: 30px;
    right: 30px;

    &__btn {
      text-align: right;

      button {
        background-color: transparent;
        padding: 0;
        border: none;
        width: 20px;
        height: 20px;
        cursor: pointer;

        svg {
          width: 100%;
          height: 100%;

          path {
            fill: #aaa;
          }
        }
      }

    }

    &__box {
      max-width: 600px;
      width: calc(100vw - 60px);
      border: 1px solid #ccc;
      padding: 40px;
      background-color: #fff;

      .card {
        cursor: normal;
        transition: background-color .5s;

        &:hover {
          background-color: #fff;
        }

        &.active {
          background-color: #ffc;
        }
      }
    }

    &__title {
      margin-bottom: 40px;
    }

    &__section {
      button {
        background: transparent;
        padding: 0;
        border: 0;
      }
    }
  }
  </style>
