<template>
  <div>
    <HeaderText />
    <div>
      <div class="circle" ref="cir" @mousemove="skew"></div>
      <div class="square" ref="squ" @mousemove="skew"></div>
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
      const x = e.pageX - this.$refs.cir.offsetLeft;
      const y = e.pageY - this.$refs.cir.offsetTop;
      this.$refs.cir.style.setProperty("--x", x + "px");
      this.$refs.cir.style.setProperty("--y", y + "px");
      console.log(e.clientY);
    },
  },
};
</script>

<style scoped>
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
.circle::before {
  --size: 0;
  content: "";
  position: absolute;
  left: var(--x);
  top: var(--y);
  width: 100px;
  height: 100px;
  filter: brightness(1.2) contrast(100);
  opacity: 0.4;
  background: radial-gradient(circle closest-side, #a3b1f1, transparent);
  transform: translate(-50%, -50%);
  transition: all 0.2s ease, left 0s, top 0s;
}
.circle:hover::before {
  --size: 200px;
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
