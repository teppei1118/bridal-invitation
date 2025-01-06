<template>
  <section>
    <img
      :src="require('@/assets/images/211.jpg')"
      alt="introduction_01"
      class="img-fluid img-thumbnail"
    />
    <p class="mt-3" v-html="message"></p>
  </section>
</template>

<script>
export default {
  data() {
    return {
      message: `謹啓
                向春の候 皆様にはますますご清祥のことと
                お慶び申し上げます

                さて このたび 私どもの婚約が整い
                結婚式を挙げることとなりました

                つきましては
                幾久しくご懇情を賜りたく
                披露かたがた小宴をもうけますので
                誠に恐縮ではございますが
                なにとぞご光臨の栄を賜りますようご案内申し上げます

                謹白

                2025年2月吉日
                山下 哲平  石橋 さくら
              `,
    };
  },
};
</script>

<style scoped></style>
