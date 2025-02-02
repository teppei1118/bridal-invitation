<template>
  <div class="attendance-container" @click="handleClick">
    <img :src="currentImage" alt="attendance" class="attendance-image" />
  </div>
</template>
<script>
export default {
  data() {
    return {
      defaultImage: require('@/assets/images/attendance_init.jpg'),
      attendImage: require('@/assets/images/attendance_attend.jpg'),
      absentImage: require('@/assets/images/attendance_absent.jpg'),
      currentImage: require('@/assets/images/attendance_init.jpg'),
    };
  },
  methods: {
    handleClick(event) {
      const clickX = event.offsetX;
      const elementWidth = event.currentTarget.clientWidth;

      if (clickX < elementWidth / 2) {
        // 左半分をクリック → 出席
        this.currentImage = this.attendImage;
        this.$emit('update:attendance', 'attend');
      } else {
        // 右半分をクリック → 欠席
        this.currentImage = this.absentImage;
        this.$emit('update:attendance', 'absent');
      }
    },
  },
};
</script>

<style scoped>
.attendance-container {
  width: 100%;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}

.attendance-image {
  width: 100%;
  max-width: 400px; /* 必要に応じて調整 */
}
</style>
