<template>
  <div class="col">
    <label :for="id" class="form-label">{{ this.label }}</label>
    <input
      class="form-control"
      :type="this.type"
      :name="this.name"
      :id="this.id"
      :placeholder="this.placeholder ?? this.label"
      :value="value"
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
    value: {
      type: String,
      default: '',
    },
    type: {
      type: String,
      default: 'text',
    },
  },
};
</script>

<style></style>
