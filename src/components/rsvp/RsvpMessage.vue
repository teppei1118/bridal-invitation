<template>
  <p class="fs-6 pt-4" v-html="message"></p>
</template>

<script>
export default {
  data() {
    return {
      message: `郵送でのご案内状に代わり
                当招待状をお送りしております

                お手数ではございますが
                出席情報のご登録をお願い申し上げます

                返信は2025年3月21日までにお願いします`,
    };
  },
  props: {
    deadline: {
      required: true,
      type: String,
    },
  },
};
</script>

<style scoped></style>
