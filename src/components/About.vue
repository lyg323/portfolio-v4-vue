<template>
  <section id="about" class="section about">
    <div class="about-container">
      <div class="about-inner">
        <div class="about-title-wrap">
          <div class="about-title">
            <h2>About <br /><i>Me</i></h2>
            <p>
              7년차 웹 퍼블리셔 이영경입니다.<br />
              새로운 기술을 배우는 것을 좋아하고 빠르게 습득합니다.<br />
              앞으로도 새로운 도전과 기회를 통해 성장해 나가고자 합니다.
            </p>
          </div>
          <div class="about-detail">
            <h3>Work<br />Experience</h3>
            <div class="about-detail-list">
              <ul>
                <li>
                  <span>2024</span>
                  <p>삼성카드 데이터랩 구축</p>
                </li>
                <li>
                  <span>2023</span>
                  <p>삼성카드 운영</p>
                  <p>윙고 선거문자 구축</p>
                </li>
                <li>
                  <span>2022</span>
                  <p>삼성카드 운영</p>
                </li>
                <li>
                  <span>2021</span>
                  <p>삼성카드 운영</p>
                  <p>펫팟 구축</p>
                </li>
              </ul>
              <ul>
                <li>
                  <span>2020</span>
                  <p>키디키디 구축</p>
                  <p>펫팟 구축</p>
                  <p>이랜드리테일 운영</p>
                </li>
                <li>
                  <span>2019</span>
                  <p>이랜드리테일 앱 구축</p>
                  <p>스마일게이트 운영</p>
                  <p>WCG 구축 및 운영</p>
                  <p>이랜드잇, 이랜드복지재단, 이랜드호텔 운영</p>
                </li>
              </ul>
            </div>
          </div>
        </div>
        <ul class="about-skill-wrap">
          <li class="about-skill" v-for="(skill, i) in skills" :key="i">
            <div class="circle circle-hover">
              <div class="circle-hover-background"></div>
              <div class="circle-content">
                <p class="circle-text circle-text-top">SKILL</p>
                <p class="circle-title">{{ skill.title }}</p>
                <p class="circle-text circle-text-bottom" v-if="skill.text">
                  {{ skill.text }}
                </p>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted, ref } from 'vue';

const skills = ref([
  { title: 'HTML5' },
  { title: 'CSS3' },
  { title: 'SASS' },
  { title: 'SCSS', text: 'SCSS' },
  { title: 'JavaScript', text: 'ES6+' },
  { title: 'ES6+' },
  { title: 'jQuery' },
  { title: 'Vue' },
  { title: 'React' },
  { title: 'Git' },
]);

onMounted(() => {
  const aboutContainer = document.querySelector('.about-container');
  const aboutInner = document.querySelector('.about-inner');
  const aboutSkillWrap = document.querySelector('.about-skill-wrap');

  const updateHorizontalScroll = () => {
    if (window.innerWidth > 1024) {
      const containerRect = aboutContainer.getBoundingClientRect();
      aboutContainer.style.height = `${aboutSkillWrap.offsetWidth}px`;

      if (containerRect.top <= 0) {
        const translateX = Math.max(
          containerRect.top * 0.7,
          -(aboutSkillWrap.offsetWidth - window.innerWidth)
        );

        aboutInner.classList.add('about-inner-sticky');
        aboutSkillWrap.style.transform = `translateX(${translateX}px)`;
      } else {
        aboutInner.classList.remove('about-inner-sticky');
      }
    } else {
      aboutContainer.style.height = 'auto';
      aboutSkillWrap.style.transform = 'translateX(0)';
    }
  };

  updateHorizontalScroll();
  window.addEventListener('scroll', updateHorizontalScroll);
  window.addEventListener('resize', updateHorizontalScroll);
});
</script>

<style lang="scss" scoped>
.about {
  .about-inner {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: flex-start;
    min-height: 100vh;
    padding: 8rem 0;
    box-sizing: border-box;
    overflow: hidden;

    &.about-inner-sticky {
      position: sticky;
      top: 0;
    }
  }

  .about-title-wrap {
    display: flex;
    justify-content: space-between;
    width: 100%;
    padding: 0 10rem;
  }

  .about-title {
    h2 {
      font-size: 5vw;
      line-height: 1;

      i {
        font-style: italic;
      }
    }

    p {
      margin-top: 5rem;
      color: $color-gray;
      font-size: 2rem;
      line-height: 1.4;
      word-break: keep-all;
    }
  }

  .about-detail {
    display: flex;
    justify-content: space-between;
    gap: 10rem;
    width: 50%;
    margin-top: 2rem;

    h3 {
      flex-shrink: 0;
      font-size: 3rem;
      font-weight: 500;
    }

    .about-detail-list {
      flex-grow: 1;
      display: flex;

      ul {
        width: 50%;
      }

      li {
        margin-bottom: 2rem;
      }
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

  .about-skill-wrap {
    display: flex;
    flex-wrap: nowrap;
    justify-content: flex-start;
    align-items: flex-end;
    gap: 5rem;
    padding: 0 10rem;
    transition: transform 0.2s linear;
  }

  .about-skill {
    flex-shrink: 0;
    box-sizing: border-box;

    &:nth-child(3n) {
      margin-bottom: 20rem;
    }
  }

  @include media-small-down {
    .about-inner {
      gap: 5rem;
      min-height: auto;
    }

    .about-title {
      h2 {
        font-size: 8rem;
      }
    }

    .about-title-wrap {
      flex-direction: column;
      padding: 0 2rem;
    }

    .about-detail {
      flex-direction: column;
      gap: 5rem;
      width: 100%;
      margin-top: 5rem;
    }

    .about-skill-wrap {
      flex-wrap: wrap;
      justify-content: center;
      align-items: flex-start;
      gap: 2rem;
      padding: 0 2rem;
    }

    .about-skill:nth-child(3n) {
      margin-bottom: 0;
    }
  }
}
</style>
