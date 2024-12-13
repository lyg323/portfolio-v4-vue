<template>
  <header class="header">
    <div class="header-logo-area">
      <h1 class="header-logo"><a href="/">이영경</a></h1>
      <a
        class="header-link"
        href="https://github.com/lyg323"
        target="_blank"
        title="github"
      >
        <i class="icon icon-github-mark"></i>
      </a>
    </div>
    <div class="header-nav-area">
      <nav class="header-nav">
        <ul>
          <li>
            <a href="#about">ABOUT</a>
          </li>
          <li>
            <a href="#project">PROJECT</a>
          </li>
        </ul>
      </nav>
      <button
        @click="toggleDarkMode"
        type="button"
        class="header-theme"
        :title="isDark ? 'Light Mode' : 'Dark Mode'"
      ></button>
    </div>
  </header>
</template>

<script setup>
import { onMounted, ref } from 'vue';

const isDark = ref(JSON.parse(localStorage.getItem('isDark')) || false);
const buttonTheme = ref(null);

const initDarkMode = () => {
  document.documentElement.classList.toggle('dark', isDark.value);
  buttonTheme.value.title = isDark.value ? 'Light Mode' : 'Dark Mode';
};

const toggleDarkMode = () => {
  isDark.value = !isDark.value;
  localStorage.setItem('isDark', JSON.stringify(isDark.value));
  initDarkMode();
};

onMounted(() => {
  buttonTheme.value = document.querySelector('.header-theme');
  initDarkMode();
});
</script>

<style lang="scss" scoped>
.header {
  position: fixed;
  left: 0;
  top: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 10rem;
  padding: 0 10rem;
  z-index: $zindex-fixed;

  .header-logo-area {
    display: flex;
    gap: 10rem;
    align-items: center;
  }

  .header-logo {
    font-size: 1.8rem;
    font-weight: 500;
  }

  .header-link {
    line-height: 0;
  }

  .header-time {
    color: $color-gray;
    font-size: 1.8rem;
  }

  .header-nav-area {
    display: flex;
    gap: 10rem;
  }

  .header-nav {
    ul {
      display: flex;
      gap: 5rem;
    }

    li {
      color: $color-gray;
      font-size: 1.8rem;
    }
  }

  .header-theme {
    display: inline-block;
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    background: $color-black;
  }

  @include media-small-down {
    height: 8rem;
    padding: 0 2rem;

    .header-logo-area {
      gap: 2rem;
    }

    .header-time {
      display: none;
    }

    .header-nav-area {
      gap: 2rem;
    }

    .header-nav ul {
      gap: 2rem;
    }
  }
}
</style>
