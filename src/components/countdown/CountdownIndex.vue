<template>
  <section id="countdown" class="">
    <div class="rounded-3 bg-navy lh-1">
      <div class="container p-5">
        <h2>COUNTDOWN</h2>
        <div class="pt-4">
          <div class="fs-countdown-days number">{{ days }}</div>
          <div class="fs-4">DAYS</div>
        </div>
        <div class="row pt-3">
          <div class="col">
            <div class="fs-1 number">{{ hours }}</div>
            <div>HOUR.</div>
          </div>
          <div class="col">
            <div class="fs-1 number">{{ minutes }}</div>
            <div>MIN.</div>
          </div>
          <div class="col">
            <div class="fs-1 number">{{ seconds }}</div>
            <div>SEC.</div>
          </div>
        </div>
        <div class="fs-2 pt-4">{{ formattedDeadline }}</div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      days: '00',
      hours: '00',
      minutes: '00',
      seconds: '00',
    };
  },
  mounted() {
    this.startCountdown();
  },
  methods: {
    startCountdown() {
      setInterval(() => {
        const now = new Date().getTime();
        const targetDate = new Date(this.deadline).getTime();
        const distance = targetDate - now;

        if (distance > 0) {
          this.days = String(
            Math.floor(distance / (1000 * 60 * 60 * 24))
          ).padStart(2, '0');
          this.hours = String(
            Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
          ).padStart(2, '0');
          this.minutes = String(
            Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60))
          ).padStart(2, '0');
          this.seconds = String(
            Math.floor((distance % (1000 * 60)) / 1000)
          ).padStart(2, '0');
        } else {
          // TODO: タイムアップの仕組み
        }
      }, 1000); // 毎秒更新
    },
  },
  props: {
    deadline: {
      required: true,
      type: String,
    },
  },
  computed: {
    formattedDeadline() {
      const date = new Date(this.deadline);
      return `${date.getFullYear()}.${String(date.getMonth() + 1).padStart(
        2,
        '0'
      )}.${String(date.getDate()).padStart(2, '0')}`;
    },
  },
};
</script>

<style></style>
