<template>
  <div>
    <img
      alt="groom"
      :src="require('@/assets/images/groom.jpg')"
      class="mx-auto d-block rounded-circle"
    />
  </div>
  <h3 class="text-center pt-3">Groom</h3>
  <div class="fs-5">山下 哲平</div>
  <p v-html="message"></p>
</template>

<script>
export default {
  data() {
    return {
      message: `
        この度晴れてさくらさんと
        結婚することとなりました

        今後とも新郎新婦共々
        宜しくお願いします
      `,
    };
  },
};
</script>

<style scoped></style>
