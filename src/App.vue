<template>
  <InviteIndex :deadline="'2025-04-26'"></InviteIndex>
</template>

<script>
import InviteIndex from './components/InviteIndex.vue';

export default {
  name: 'App',
  components: {
    InviteIndex,
  },
};

document.addEventListener('DOMContentLoaded', () => {
  const sections = document.querySelectorAll('div'); // section要素を取得

  const onScroll = () => {
    const windowHeight = window.innerHeight;

    sections.forEach((section) => {
      const sectionTop = section.getBoundingClientRect().top;

      if (sectionTop < windowHeight - 50) {
        section.classList.add('visible');
      }
    });
  };

  window.addEventListener('scroll', onScroll);
  onScroll(); // 初回チェック
});
</script>

<style>
/* Fonts */
@import url('https://fonts.bunny.net/css?family=Nunito');

/* Bootstrap */
@import url('https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css');

/* font */
@import url('https://use.typekit.net/hxo7pbg.css');

body {
  color: #2d3c67;
  background-color: #f2ecff;
  text-align: center;
  white-space: pre-line;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  word-break: break-all;
  font-family: 'aria-text-g2', 'source-han-serif-jp-subset', sans-serif;
  font-weight: 400;
  font-style: normal;
}

#all {
  width: 100%;
  max-width: 768px;
  margin: 0 auto; /* 横方向の中央揃え */
  box-sizing: border-box;
}

@media screen and (min-width: 768px) {
  #all {
    width: 768px;
  }
}

h2,
h3 {
  font-family: 'gloock', sans-serif;
  font-weight: 400;
  font-style: normal;
}

img {
  width: 100%;
}

section {
  padding: 50px 25px;
}

div {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 1s ease, transform 2s ease;
}

div.visible {
  opacity: 1;
  transform: translateY(0);
}

.bg-navy {
  color: #eaf6ff;
  background-color: #2d3c67;
}

.fs-countdown-days {
  font-size: calc(1.35rem + 15vw) !important;
}

.btn-bridal {
  --bs-btn-color: #f2ecff;
  --bs-btn-bg: #2d3c67;
  --bs-btn-border-color: #2d3c67;
  --bs-btn-hover-color: #f2ecff;
  --bs-btn-hover-bg: #2d3c67;
  --bs-btn-hover-border-color: #2d3c67;
  --bs-btn-focus-shadow-rgb: 211, 212, 213;
  --bs-btn-active-color: #f2ecff;
  --bs-btn-active-bg: #2d3c67;
  --bs-btn-active-border-color: #2d3c67;
  --bs-btn-active-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  --bs-btn-disabled-color: #f2ecff;
  --bs-btn-disabled-bg: #2d3c67;
  --bs-btn-disabled-border-color: #2d3c67;
}
</style>
