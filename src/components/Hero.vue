<template>
  <section class="section hero">
    <div class="hero-title">
      <h2>Portfolio</h2>
      <p>ⓒ 2024 이영경</p>
    </div>
    <div class="circle circle-fixed hero-circle">
      <svg class="circle-img" viewBox="0 0 100 100">
        <circle class="circle-frame" cx="50" cy="50" r="49.5" />
        <circle class="circle-bar" cx="50" cy="50" r="49.5" />
      </svg>
      <span class="circle-line"></span>
      <div class="circle-content">
        <p class="circle-title">안녕하세요!</p>
      </div>
    </div>
  </section>
</template>

<script setup></script>

<style lang="scss" scoped>
.hero {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;

  .hero-title {
    padding-bottom: 10rem;

    h2 {
      font-size: 7vw;
      font-style: italic;
    }

    p {
      margin-top: 10rem;
      color: $color-gray;
      font-size: 1.8rem;
      text-align: center;
    }
  }

  @include media-small-down {
    .hero-title {
      padding-bottom: 0;

      h2 {
        font-size: 8rem;
      }

      p {
        margin-top: 5rem;
      }
    }
  }
}
</style>
