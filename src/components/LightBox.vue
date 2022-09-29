<template>
  <div class="light-box">
    <div :class="active === 0 ? 'active' : ''" @click="makeActive(0)">
      {{ model[0] }}
    </div>
    <div :class="active === 1 ? 'active' : ''" @click="makeActive(1)">
      {{ model[1] }}
    </div>
    <div :class="active === 2 ? 'active' : ''" @click="makeActive(2)">
      {{ model[2] }}
    </div>
  </div>
</template>

<script>
export default {
  name: "LightBox",
  props: ["model"],
  data() {
    return {
      active: 0,
    };
  },
  watch: {
    "$attrs.value": function (number) {
      this.active = number;
    },
  },
  methods: {
    makeActive(number) {
      this.active = number;
      this.emitCurrentIndex(number);
    },
    emitCurrentIndex(number) {
      this.$emit("input", number);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.light-box {
  border: 10px solid #ccc;
  border-radius: 1rem;
  display: grid;
  grid-template-rows: repeat(3, minmax(0, 1fr));
  grid-gap: 10px;
  background: #ccc;
  height: calc(3 * 5rem + 4 * 10px);
  width: calc(10px * 2 + 8 * 3rem);

  > div {
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    border: none;
    overflow: hidden;
    padding-left: 0.75em;

    transition: 0.5s;
    background: #fff;

    letter-spacing: 1.9rem;
    white-space: nowrap;

    font-size: 2.75rem;
    font-family: "Barlow Condensed", monospace;

    &:last-child {
      border: none;
    }

    &.active {
      background: #ffffdd;
    }
  }
}
</style>
