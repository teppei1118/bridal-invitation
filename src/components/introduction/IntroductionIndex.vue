<template>
  <section>
    <img
      :src="require('@/assets/images/introduction_01.jpg')"
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
                向春の候 皆様には
                ますますご清祥のことと
                お慶び申し上げます

                このたび 私たちは
                結婚式を挙げることと
                なりました

                つきましては
                日頃お世話になっている皆様に
                感謝を込めて ささやかながら
                結婚披露宴を行いたいと思います

                お忙しい中
                誠に恐縮でございますが
                ぜひご出席をいただきたく
                ご案内申し上げます

                謹白

                2025年2月吉日
                山下 哲平  石橋 さくら
              `,
    };
  },
};
</script>

<style scoped></style>
