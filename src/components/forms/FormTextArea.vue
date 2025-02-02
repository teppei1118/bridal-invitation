<template>
  <div class="col">
    <label :for="id" class="form-label">{{ label }}</label>
    <textarea
      class="form-control"
      :type="type"
      :name="name"
      :id="id"
      :placeholder="placeholder"
      :value="modelValue"
      :rows="rows"
      @input="$emit('update:modelValue', $event.target.value)"
    />
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
    rows: {
      type: String,
      default: '3',
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

<style></style>
