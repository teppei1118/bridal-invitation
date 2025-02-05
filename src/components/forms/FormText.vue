<template>
  <div class="col" :class="{ visible: visible }">
    <label :for="id" class="form-label">{{ label }}</label>
    <input
      class="form-control"
      :type="type"
      :name="name"
      :id="id"
      :placeholder="placeholder ?? label"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
      :class="{
        'is-invalid': errorMessage !== '',
      }"
      @blur="validate"
    />
    <div v-if="errorMessage !== ''" class="invalid-feedback text-break visible">
      {{ this.errorMessage }}
    </div>
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
    visible: {
      type: Boolean,
      default: false,
    },
    validation: {
      type: Array,
      default: () => [],
    },
  },
  emits: ['update:modelValue'],
  data() {
    return {
      errorMessage: '',
    };
  },
  methods: {
    validate() {
      this.errorMessage = '';
      // 必須
      if (this.validation.includes('required') && !this.modelValue) {
        this.errorMessage =
          this.errorMessage !== ''
            ? this.errorMessage
            : `${this.label}は必須です。`;
      }
      // カナ入力
      if (
        this.validation.includes('kana') &&
        !/^[\p{Script=Hiragana}\p{Script=Katakana}ー々]+$/u.test(
          this.modelValue
        )
      ) {
        this.errorMessage =
          this.errorMessage !== ''
            ? this.errorMessage
            : `${this.label}はカナで入力してください。`;
      }
      // メールアドレス
      if (
        this.validation.includes('email') &&
        !/^[A-Za-z0-9]{1}[A-Za-z0-9_.-]*@{1}[A-Za-z0-9_.-]{1,}\.[A-Za-z0-9]{1,}$/.test(
          this.modelValue
        )
      ) {
        this.errorMessage =
          this.errorMessage !== ''
            ? this.errorMessage
            : `メールアドレスが正しくありません。`;
      }
      // 全角文字
      if (
        this.validation.includes('zenkaku') &&
        // eslint-disable-next-line no-control-regex
        !/^[^\x01-\x7E\xA1-\xDF]*$/.test(this.modelValue)
      ) {
        this.errorMessage =
          this.errorMessage !== ''
            ? this.errorMessage
            : `${this.label}は全角文字のみで入力してください。`;
      }
      // 半角文字
      if (
        this.validation.includes('hankaku') &&
        /[^\x20-\x7E]/.test(this.modelValue)
      ) {
        this.errorMessage =
          this.errorMessage !== ''
            ? this.errorMessage
            : `${this.label}は半角文字のみで入力してください。`;
      }
      // 半角数値
      if (
        this.validation.includes('hankaku-numeric') &&
        !/^[0-9]+$/.test(this.modelValue)
      ) {
        this.errorMessage =
          this.errorMessage !== ''
            ? this.errorMessage
            : `${this.label}は半角数値のみで入力してください。`;
      }

      return this.errorMessage === '';
    },
  },
  watch: {
    modelValue() {
      this.errorMessage = '';
    },
  },
};
</script>
