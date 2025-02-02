<template>
  <div class="form-check">
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
  },
  emits: ['update:checked'],
};
</script>

<style></style>
