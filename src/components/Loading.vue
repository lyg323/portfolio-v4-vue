<template>
  <div class="loading">
    <div class="circle circle-fixed">
      <svg class="circle-img" viewBox="0 0 100 100">
        <circle class="circle-frame" cx="50" cy="50" r="49.5" />
        <circle class="circle-bar" cx="50" cy="50" r="49.5" />
      </svg>
      <span class="circle-line"></span>
      <div class="circle-content">
        <p class="circle-percent">0%</p>
      </div>
    </div>
  </div>
</template>

<script setup></script>

<style lang="scss" scoped>
.loading {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  z-index: $zindex-fixed;
  background: $color-white;
  pointer-events: none;
  transition: opacity 1s, visibility 2s;
  transition-delay: 1s;

  &.hide {
    opacity: 0;
    visibility: hidden;
  }
}
</style>
