<template>
  <div>
    <HeaderText />
    <div>
      <div class="circle" ref="cir" @mousemove="skew"></div>
      <div class="square" ref="squ" @mousemove="skew"></div>
      <div class="cursor" ref="cur" @mousemove="curs"></div>
    </div>
  </div>
</template>
<script>
import HeaderText from "../components/HeaderText.vue";
export default {
  name: "main-view",
  components: { HeaderText },
  data() {
    return {
      sampleData: "",
    };
  },
  setup() {},
  beforeCreate() {},
  created() {},
  beforeMount() {},
  mounted() {},
  beforeUpdate() {},
  updated() {},
  beforeUnmount() {},
  unmounted() {},
  methods: {
    skew: function (e) {
      this.$refs.cir.style.setProperty("--mouse-x", e.clientX);
      this.$refs.cir.style.setProperty("--mouse-y", e.clientY);
      this.$refs.squ.style.setProperty("--mouse-x", e.clientX);
      this.$refs.squ.style.setProperty("--mouse-y", e.clientY);
      console.log(e.clientY);
    },
    curs: function (e) {
      let x = e.pageX;
      let y = e.pageY;
      this.$refs.cur.style.top = y + "px";
      this.$refs.cur.style.left = x + "px";
    },
  },
};
</script>

<style scoped>
.cursor {
  z-index: 999;
  position: fixed;
  background-color: blue;
  width: 20px;
  height: 20px;
  border-radius: 50px;
  box-shadow: 0 0 20px blue, 0 0 60px blue, 0 0 100px blue;
}
.cursor:before {
  content: "";
  position: absolute;
  background-color: blue;
  width: 50px;
  height: 50px;
  opacity: 0.2;
  transform: translate(-50%, -30%);
  border-radius: 50%;
}
.circle {
  width: 150px;
  height: 150px;
  background-color: rosybrown;
  position: relative;
  bottom: -30px;
  filter: drop-shadow(0 15px 15px rgba(0, 0, 0, 0.3)) contrast(500%);
  transform: perspective(150px) rotateX(calc((var(--mouse-y) - 200) * -0.1deg))
    rotateY(calc((var(--mouse-x) - 70) * 0.1deg));
  transition: transform 0.5 ease;
  animation: animateColor 5s linear infinite;
}
.square {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100px;
  height: 100px;
  background-color: red;
  filter: drop-shadow(0 15px 15px rgba(0, 0, 0, 0.3));
  transform: perspective(150px) rotateX(calc((var(--mouse-y) - 200) * -0.1deg))
    rotateY(calc((var(--mouse-x) - 70) * 0.1deg));
  transition: transform 1 ease;
  animation: animateColor 5s linear infinite;
  /* calc((var(--mouse-x)) * 0.1deg)  10, -10  7~100 사이를 -10~10 사이로 만들어야 함 */
}
@keyframes animateColor {
  0% {
    filter: hue-rotate(0deg);
  }
  100% {
    filter: hue-rotate(350deg);
  }
}
</style>
