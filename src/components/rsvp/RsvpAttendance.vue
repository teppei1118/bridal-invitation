<template>
  <div class="attendance-area" @click="handleClick" @blur="validate">
    <img :src="currentImage" alt="attendance" class="attendance-image" />
  </div>
  <div v-if="errorMessage !== ''" class="text-danger text-start fs-6 visible">
    {{ errorMessage }}
  </div>
</template>
<script>
export default {
  props: {
    attendance: {
      type: [Boolean, null],
      default: null,
    },
  },
  data() {
    return {
      defaultImage: require('@/assets/images/attendance_init.png'),
      attendImage: require('@/assets/images/attendance_attend.jpg'),
      absentImage: require('@/assets/images/attendance_absent.jpg'),
      errorMessage: '',
    };
  },
  computed: {
    currentImage() {
      if (this.attendance === true) {
        return this.attendImage;
      } else if (this.attendance === false) {
        return this.absentImage;
      } else {
        return this.defaultImage;
      }
    },
  },
  methods: {
    handleClick(event) {
      const clickX = event.offsetX;
      const elementWidth = event.currentTarget.clientWidth;
      const newAttendance = clickX < elementWidth / 2;

      this.$emit('update:attendance', newAttendance);
    },
    validate() {
      this.errorMessage = this.attendance === null ? '出欠は必須です。' : '';
      return this.errorMessage === '';
    },
  },
};
</script>

<style scoped>
.attendance-area {
  width: 100%;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}

.attendance-image {
  width: 100%;
}
</style>
