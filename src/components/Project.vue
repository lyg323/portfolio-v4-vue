<template>
  <section id="project" class="section project">
    <ul class="project-list">
      <li class="project-item" v-for="(project, i) in data" :key="project.id">
        <div class="project-title">
          <h2>{{ project.name }}</h2>
          <p>{{ project.role }}</p>
          <a class="button project-button" :href="project.link" target="_blank">
            <span>VISIT</span>
            <i class="icon icon-arrow-out"></i>
          </a>
        </div>
        <div class="project-image-wrap">
          <div
            class="project-image project-image-pc project-image-slide"
            v-if="project.imgPc1"
          >
            <img
              :src="`./src/${src}`"
              alt=""
              v-for="(src, i) in project.imgPc1"
              :key="i"
              :class="{ active: i === 0 }"
            />
          </div>
          <div
            class="project-image project-image-mobile project-image-slide"
            v-if="project.imgMo1"
          >
            <img
              :src="'./src/' + src"
              alt=""
              v-for="(src, i) in project.imgMo1"
              :key="i"
              :class="{ active: i === 0 }"
            />
          </div>
          <div
            class="project-image project-image-mobile project-image-slide"
            v-if="project.imgMo2"
          >
            <img
              :src="'./src/' + src"
              alt=""
              v-for="(src, i) in project.imgMo2"
              :key="i"
              :class="{ active: i === 0 }"
            />
          </div>
          <div
            class="project-image project-image-mobile project-image-slide"
            v-if="project.imgMo3"
          >
            <img
              :src="'./src/' + src"
              alt=""
              v-for="(src, i) in project.imgMo3"
              :key="i"
              :class="{ active: i === 0 }"
            />
          </div>
          <div
            class="project-image project-image-mobile project-image-slide"
            v-if="project.imgMo4"
          >
            <img
              :src="'./src/' + src"
              alt=""
              v-for="(src, i) in project.imgMo4"
              :key="i"
              :class="{ active: i === 0 }"
            />
          </div>
        </div>
        <div class="project-desc">
          <p class="project-number">
            <span class="project-number-current">{{ i + 1 }}</span>
            <i> / </i>
            <span class="project-number-total">{{ data.length }}</span>
          </p>
          <ul class="project-desc-list">
            <li>
              <span>스킬</span>
              <p>{{ project.skill }}</p>
            </li>
            <li>
              <span>기간</span>
              <p>{{ project.period }}</p>
            </li>
            <li>
              <span>참여도</span>
              <p>{{ project.engagement }}</p>
            </li>
          </ul>
        </div>
      </li>
    </ul>
  </section>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import { data } from '../assets/data';

const projectSlides = ref([]);

onMounted(() => {
  projectSlides.value = document.querySelectorAll('.project-image-slide');

  projectSlides.value.forEach((slide) => {
    const images = slide.querySelectorAll('img');
    let currentIndex = 0;
    let interval = null;

    const startSlide = () => {
      interval = setInterval(() => {
        images.forEach((img) => img.classList.remove('active'));
        currentIndex = currentIndex >= images.length - 1 ? 0 : currentIndex + 1;
        images[currentIndex].classList.add('active');
      }, 2500);
    };

    const stopSlide = () => clearInterval(interval);

    startSlide();
    slide.addEventListener('mouseenter', stopSlide);
    slide.addEventListener('mouseout', startSlide);
  });
});
</script>

<style lang="scss" scoped>
.project {
  min-height: 100vh;
  padding: 20rem 10rem 10rem;

  .project-item {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;

    & + .project-item {
      position: relative;
      margin-top: 10rem;
      padding-top: 10rem;

      &::after {
        content: '';
        position: absolute;
        left: 0;
        top: 0;
        display: block;
        width: 100%;
        height: 1px;
        background: $color-light-gray;
      }
    }
  }

  .project-title {
    position: sticky;
    top: 10rem;
    width: 20%;

    h2 {
      font-size: 4vw;
      font-weight: 500;
    }

    p {
      margin-top: 5rem;
      color: $color-gray;
      font-size: 2rem;
      line-height: 1.4;
      word-break: keep-all;
    }
  }

  .project-button {
    margin-top: 5rem;
  }

  .project-image-wrap {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    gap: 5rem;
    width: 40%;

    .project-image {
      display: flex;
      gap: 5rem;
      border-radius: 2rem;
      overflow: hidden;

      &-pc {
        width: 100%;

        img {
          max-height: 60rem;
        }
      }

      &-mobile {
        width: calc(50% - 2.5rem);

        img {
          max-height: 80rem;
        }
      }

      &-slide {
        position: relative;
        overflow: hidden;

        img {
          opacity: 0;
          transition: opacity 1s;

          &:not(:first-child) {
            position: absolute;
            left: 0;
            top: 0;
          }

          &.active {
            opacity: 1;
          }
        }
      }
    }

    img {
      width: 100%;
      vertical-align: top;
      object-fit: cover;
      object-position: center top;

      border-radius: 2rem;
      overflow: hidden;
    }
  }

  .project-desc {
    position: sticky;
    top: 10rem;
    width: 20%;
    padding-left: 5%;
  }

  .project-number {
    font-size: 3vw;
    font-weight: 500;

    i {
      color: $color-gray;
      font-weight: 200;
    }
  }

  .project-desc-list {
    margin-top: 5rem;

    li {
      margin-bottom: 2rem;
    }

    span {
      font-size: 1.8rem;
      font-weight: 500;
    }

    p {
      margin-top: 0.5rem;
      color: $color-gray;
      font-size: 1.8rem;
    }
  }

  @include media-small-down {
    padding: 8rem 2rem;

    .project-item {
      flex-direction: column;

      & + .project-item {
        margin-top: 5rem;
        padding-top: 5rem;
      }
    }

    .project-title {
      position: relative;
      top: 0;
      width: 100%;

      h2 {
        font-size: 8rem;
      }
    }

    .project-image-wrap {
      gap: 2rem;
      width: 100%;
      margin-top: 5rem;

      .project-image-pc img {
        max-height: none;
      }

      .project-image-mobile {
        width: calc(50% - 1rem);
      }
    }

    .project-desc {
      position: relative;
      top: 0;
      width: 100%;
      padding: 0;
    }

    .project-number {
      display: none;
    }
  }
}
</style>
