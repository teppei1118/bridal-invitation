<template>
  <section id="host">
    <div class="container">
      <div>
        <div class="text-center pt-5">
          <h2>
            HOST<br />
            <div class="fs-6">ホスト</div>
          </h2>
        </div>
      </div>
      <HostGroom></HostGroom>
      <div class="m-5"></div>
      <HostBride></HostBride>
    </div>
  </section>
</template>

<script>
import HostBride from './HostBride.vue';
import HostGroom from './HostGroom.vue';

export default {
  components: {
    HostBride,
    HostGroom,
  },
};
</script>

<style scoped></style>
