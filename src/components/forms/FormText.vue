<template>
  <div class="col">
    <label :for="id" class="form-label">{{ label }}</label>
    <input
      class="form-control"
      :type="type"
      :name="name"
      :id="id"
      :placeholder="placeholder ?? label"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
    />
  </div>
</template>

<script>
export default {
  computed: {
    id() {
      return this.name ? this.name.replace('_', '-') : '';
    },
  },
  props: {
    label: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    placeholder: {
      type: String,
      required: false,
    },
    modelValue: {
      type: String,
      default: '',
    },
    type: {
      type: String,
      default: 'text',
    },
  },
  emits: ['update:modelValue'],
};
</script>
