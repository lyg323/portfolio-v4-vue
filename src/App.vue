<template>
  <div class="wrapper">
    <Loading />
    <div class="home hide">
      <Header />
      <div class="bg">
        <div class="bg-shape bg-shape-cursor"></div>
        <div class="bg-shape bg-shape-to-bottom"></div>
        <div class="bg-shape bg-shape-to-top"></div>
        <div class="bg-shape bg-shape-to-right"></div>
        <div class="bg-shape bg-shape-to-left"></div>
      </div>
      <Hero />
      <About />
      <Project />
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import Loading from './components/Loading.vue';
import Header from './components/Header.vue';
import About from './components/About.vue';
import Project from './components/Project.vue';
import Hero from './components/Hero.vue';

const loading = ref(null);
const loadingCirclePercent = ref(null);
const loadingCircleBar = ref(null);
const home = ref(null);

const bgShapeCursor = ref(null);
const homeSection = ref(null);
const bg = ref(null);

onMounted(() => {
  document.body.classList.add('fixed');

  // Loading
  loading.value = document.querySelector('.loading');
  loadingCirclePercent.value = loading.value.querySelector('.circle-percent');
  loadingCircleBar.value = loading.value.querySelector('.circle-bar');
  home.value = document.querySelector('.home');

  let initialStrokeDashoffset =
    (loadingCircleBar.value.getTotalLength() + 1) / 10;
  let percent = 0;

  const updateLoading = () => {
    if (percent < 100) {
      percent += 1;
      let strokeDashoffsetValue = Math.ceil(
        initialStrokeDashoffset - (initialStrokeDashoffset / 100) * percent
      );

      loadingCircleBar.value.style.strokeDashoffset = `${strokeDashoffsetValue}rem`;

      setTimeout(updateLoading, 15);
    } else {
      loading.value.classList.add('hide');
      home.value.classList.remove('hide');
      document.body.classList.remove('fixed');
      document.querySelector('.hero-circle').classList.add('animation');
    }
  };

  updateLoading();

  // Cursor
  bgShapeCursor.value = document.querySelector('.bg-shape-cursor');

  window.addEventListener('mousemove', (e) => {
    bgShapeCursor.value.style.left = `${e.clientX}px`;
    bgShapeCursor.value.style.top = `${e.clientY}px`;
  });

  // Background
  homeSection.value = document.querySelectorAll('.section');
  bg.value = document.querySelector('.bg');

  const updateBgColor = () => {
    homeSection.value.forEach((section, index) => {
      const { top, bottom } = section.getBoundingClientRect();
      const isInSection = top <= 0 && bottom >= 0;

      bg.value.classList.toggle(`bg-color-${index + 1}`, isInSection);
    });
  };

  updateBgColor();
  window.addEventListener('scroll', updateBgColor);
});
</script>

<style lang="scss">
.home {
  &.hide {
    visibility: hidden;
  }
}
</style>
