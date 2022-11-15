<template>
  <section class="src-components-board">
    <div id="container">
      <div
        class="square"
        v-for="(square, index) in squares"
        :key="index"
        :style="square.style"
        @click="getStyle(square.style)"
      ></div>
    </div>
  </section>
</template>

<script>
export default {
  name: "src-components-board",
  props: ["squares", "color"],
  mounted() {},
  data() {
    return {
      menssage: "",
    };
  },
  methods: {
    getStyle(squareStyle) {
      let { backgroundColor } = squareStyle;

      if (backgroundColor === this.color) {
        this.menssage = "You Picked Right!";
        this.sendMessage();
        this.setAllColorsTo(this.color);
        this.$emit("button", "Play Again!");
        document.querySelector("#header").style.backgroundColor = this.color;
      } else {
        this.menssage = "Try Again!";
        this.sendMessage();
        squareStyle.backgroundColor = "#232323";
      }
    },
    setAllColorsTo(color) {
      this.squares.forEach(function (square) {
        square.style.backgroundColor = color;
      });
    },
    sendMessage() {
      this.$emit("message", this.menssage);
    },
  },
  computed: {},
};
</script>

<style scoped lang="css">
.square {
  width: 30%;
  background: blue;
  padding-bottom: 30%;
  float: left;
  margin: 1.66%;
  border-radius: 10%;
  transition: background 0.8s;
  -webkit-transition: background 0.8s;
  -moz-transition: background 0.8s;
}

#container {
  margin: 20px auto;
  max-width: 600px;
}
</style>
