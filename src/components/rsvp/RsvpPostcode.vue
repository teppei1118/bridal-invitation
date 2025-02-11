<template>
  <div class="col">
    <label for="postcode" class="form-label">郵便番号（ハイフンなし）</label>
    <div class="row">
      <div class="col">
        <input
          v-model="postcode"
          class="form-control"
          type="text"
          name="postcode"
          id="postcode"
          placeholder="0000000"
          maxlength="7"
          :class="{
            'is-invalid': errorMessage !== '' || failedMessage !== '',
          }"
          @input="$emit('update:modelValue', postcode)"
          @blur="validate"
        />
        <!-- バリデーションエラーを表示 -->
        <div
          v-if="errorMessage !== ''"
          class="invalid-feedback text-break visible"
        >
          {{ errorMessage }}
        </div>
        <!-- APIエラーを表示 -->
        <div
          v-if="failedMessage !== ''"
          class="invalid-feedback text-break visible"
        >
          {{ failedMessage }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      postcode: '',
      errorMessage: '',
      failedMessage: '',
    };
  },
  methods: {
    async fetchAddress() {
      this.failedMessage = ''; // エラーメッセージをリセット
      if (!/^\d{7}$/.test(this.postcode)) {
        return; // 7桁の数字でない場合はAPIを呼ばない
      }

      try {
        const response = await axios.get(
          `https://zipcloud.ibsnet.co.jp/api/search?zipcode=${this.postcode}`
        );

        // APIのレスポンスを確認
        if (response.data.results === null) {
          this.failedMessage = '存在しない郵便番号です';
          return;
        }

        // 正常に住所を取得
        this.$emit(
          'address-found',
          response.data.results[0]['address1'] +
            response.data.results[0]['address2'] +
            response.data.results[0]['address3']
        );

        this.failedMessage = ''; // API成功時はエラーメッセージをクリア
      } catch (error) {
        this.failedMessage = '住所の取得に失敗しました';
      }
    },
    validate() {
      this.errorMessage = '';

      // 必須チェック
      if (!this.postcode) {
        this.errorMessage =
          this.errorMessage !== '' ? this.errorMessage : `郵便番号は必須です`;
      }
      // 半角数字チェック
      else if (!/^[0-9]+$/.test(this.postcode)) {
        this.errorMessage =
          this.errorMessage !== ''
            ? this.errorMessage
            : `郵便番号は半角数値のみで入力してください`;
      }
      // 桁数チェック
      else if (this.postcode.length !== 7) {
        this.errorMessage =
          this.errorMessage !== ''
            ? this.errorMessage
            : `郵便番号は7桁で入力してください`;
      }

      return this.errorMessage === '';
    },
  },
  watch: {
    postcode(newVal) {
      if (newVal.length === 7) {
        this.fetchAddress();
      }
    },
  },
  emits: ['update:modelValue', 'address-found'],
};
</script>
