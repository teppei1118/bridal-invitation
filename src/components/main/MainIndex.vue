<template>
  <div id="main" class="vh-100 position-relative text-white">
    <img
      :src="require('@/assets/images/main_flame.png')"
      alt="main-frame"
      class="frame"
    />
    <img
      :src="require('@/assets/images/main_name.png')"
      alt="main_name"
      class="name"
    />
    <img
      :src="require('@/assets/images/main_navi.png')"
      alt="main-navi"
      class="navi"
    />
  </div>
</template>

<script></script>

<style>
#main {
  background: url('@/assets/images/main_background.jpg') no-repeat center center;
  background-size: cover;
}

.frame {
  position: absolute;
  left: 0;
  top: 0;
}
.name {
  position: absolute;
  right: 0;
  left: 0;
  bottom: 0;
  margin: 0 auto;
}
.navi {
  position: absolute;
  right: 0;
  left: 0;
}
</style>
