<script setup>
import { onMounted } from 'vue';
import Loading from './components/Loading.vue';
import Header from './components/Header.vue';
import About from './components/About.vue';
import Project from './components/Project.vue';
import Hero from './components/Hero.vue';

onMounted(() => {
  // Loading
  const loading = document.querySelector('.loading');
  const loadingCirclePercent = loading.querySelector('.circle-percent');
  const loadingCircleBar = loading.querySelector('.circle-bar');
  const home = document.querySelector('.home');
  const initialStrokeDashoffset = (loadingCircleBar.getTotalLength() + 1) / 10;
  let percent = 0;

  const updateLoading = () => {
    if (percent < 100) {
      percent += 1;
      let strokeDashoffsetValue = Math.ceil(
        initialStrokeDashoffset - (initialStrokeDashoffset / 100) * percent
      );

      loadingCirclePercent.textContent = `${percent}%`;
      loadingCircleBar.style.strokeDashoffset = `${strokeDashoffsetValue}rem`;

      setTimeout(updateLoading, 25);
    } else {
      loading.classList.add('hide');
      home.classList.remove('hide');
      document.body.classList.remove('fixed');
      document.querySelector('.hero-circle').classList.add('animation');
    }
  };

  updateLoading();

  // Cursor
  const bgShapeCursor = document.querySelector('.bg-shape-cursor');

  window.addEventListener('mousemove', (e) => {
    bgShapeCursor.style.left = `${e.clientX}px`;
    bgShapeCursor.style.top = `${e.clientY}px`;
  });

  // Background
  const homeSection = document.querySelectorAll('.section');
  const bg = document.querySelector('.bg');

  const updateBgColor = () => {
    homeSection.forEach((section, index) => {
      const { top, bottom } = section.getBoundingClientRect();
      const isInSection = top <= 0 && bottom >= 0;

      bg.classList.toggle(`bg-color-${index + 1}`, isInSection);
    });
  };

  updateBgColor();
  window.addEventListener('scroll', updateBgColor);

  // Dark mode
  const buttonTheme = document.querySelector('.header-theme');
  let isDark = JSON.parse(localStorage.getItem('isDark')) || false;

  const initDarkMode = () => {
    document.documentElement.classList.toggle('dark', isDark);
    buttonTheme.querySelector('span').textContent = isDark
      ? 'Light Mode'
      : 'Dark Mode';
  };

  const toggleDarkMode = () => {
    isDark = !isDark;
    localStorage.setItem('isDark', JSON.stringify(isDark));
    initDarkMode();
  };

  initDarkMode();
  buttonTheme.addEventListener('click', toggleDarkMode);
});
</script>

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

<style lang="scss">
.home {
  &.hide {
    visibility: hidden;
  }
}
</style>
