<template>
  <div>
    <HeaderText />
    <div>
      <div class="circle" ref="cir" @mousemove="trans"></div>
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
    trans: function (e) {
      this.$refs.cir.style.setProperty("--mouse-x", e.clientX);
      this.$refs.cir.style.setProperty("--mouse-y", e.clientY);
    },
    skew: function (e) {
      this.$refs.squ.style.setProperty("--mouse-x", e.clientX);
      this.$refs.squ.style.setProperty("--mouse-y", e.clientY);
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
  transform-origin: center;
  transform: translateX(calc(var(--mouse-x) * 0.3px))
    translateY(calc(var(--mouse-y) * 0.1px));
  transition: transform 0.5 ease;
}
.square {
  width: 100px;
  height: 100px;
  background-color: red;
  transform: perspective(150px) rotateX(calc(var(--mouse-y) * 0.1deg));
  /* transition: transform 0.5 ease; */
}
</style>
