<template>
  <div>
    <img
      alt="groom"
      :src="require('@/assets/images/bride.jpg')"
      class="mx-auto d-block rounded-circle"
    />
  </div>
  <h3 class="text-center pt-3">Bride</h3>
  <div class="fs-5">石橋 さくら</div>
  <p v-html="message"></p>
</template>

<script>
export default {
  data() {
    return {
      message: `
        サクラでーす

        よろしく！
      `,
    };
  },
};
</script>

<style scoped></style>
