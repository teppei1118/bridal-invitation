<template>
  <div class="col" :class="{ visible: visible }">
    <div class="form-check" :class="{ visible: visible }">
      <input
        class="form-check-input"
        type="checkbox"
        :name="name"
        :id="id"
        :value="value"
        :checked="checked"
        @change="$emit('update:checked', $event.target.checked)"
      />
      <label class="form-check-label" for="flexCheckDefault">
        {{ this.label }}
      </label>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    id: function () {
      return this.name.replace('_', '-');
    },
  },
  props: {
    checked: {
      type: Boolean,
      default: false,
    },
    label: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    value: {
      type: String,
      default: '',
    },
    visible: {
      type: Boolean,
      default: false,
    },
  },
  emits: ['update:checked'],
};
</script>

<style></style>
