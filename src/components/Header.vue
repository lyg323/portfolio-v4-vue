<template>
  <header class="header">
    <div class="header-logo-area">
      <h1 class="header-logo"><a href="/">이영경</a></h1>
    </div>
    <div class="header-nav-area">
      <nav class="header-nav">
        <ul>
          <li><a href="#about">ABOUT</a></li>
          <li><a href="#project">PROJECT</a></li>
        </ul>
      </nav>
      <button type="button" class="header-theme">
        <span class="blind">Dark Mode</span>
      </button>
    </div>
  </header>
</template>

<script setup>
import { onMounted } from 'vue';

onMounted(() => {
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
  }

  .header-logo {
    font-size: 1.8rem;
    font-weight: 500;
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
