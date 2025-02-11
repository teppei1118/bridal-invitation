<template>
  <div class="row" :class="{ visible: visible }">
    <div class="col" :class="{ visible: visible }">{{ label }}</div>
  </div>
  <div class="row" :class="{ visible: visible }">
    <div class="col" :class="{ visible: visible }">
      <div class="btn-group" role="group" :class="{ visible: visible }">
        <template v-for="(optionLabel, key) in options" :key="key">
          <input
            type="radio"
            class="btn-check"
            :id="'radio-' + key"
            :value="key"
            autocomplete="off"
            v-model="selectedValue"
            :name="name"
          />
          <label class="btn btn-bridal-primary" :for="'radio-' + key">
            {{ optionLabel }}
          </label>
        </template>
      </div>
    </div>
    <div v-if="errorMessage !== ''" class="text-danger text-start fs-6 visible">
      {{ errorMessage }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: String,
      default: '',
    },
    options: {
      type: Object,
      default: () => {},
    },
    validation: {
      type: Array,
      default: () => [],
    },
    name: {
      type: String,
      default: '',
    },
    visible: {
      type: Boolean,
      default: false,
    },
    label: {
      type: String,
      default: '',
    },
  },
  computed: {
    selectedValue: {
      get() {
        return this.modelValue;
      },
      set(value) {
        this.$emit('update:modelValue', value);
      },
    },
  },
  data() {
    return {
      errorMessage: '',
    };
  },
  methods: {
    validate() {
      this.errorMessage = '';

      // 必須
      if (this.validation.includes('required') && this.modelValue === '') {
        this.errorMessage =
          this.errorMessage !== '' ? this.errorMessage : `ご回答は必須です`;
      }

      return this.errorMessage === '';
    },
  },
};
</script>

<style scoped>
.btn-group {
  display: flex;
  flex-wrap: wrap;
}
</style>
