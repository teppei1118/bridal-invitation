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
            'is-invalid': errorMessage !== '',
            'is-valid': errorMessage === '' && postcode.length === 7,
          }"
          @input="$emit('update:modelValue', postcode)"
        />
        <div
          v-if="this.errorMessage !== ''"
          class="invalid-feedback text-break visible"
        >
          {{ this.errorMessage }}
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
      form: [],
    };
  },
  methods: {
    async fetchAddress() {
      try {
        const response = await axios.get(
          `https://zipcloud.ibsnet.co.jp/api/search?zipcode=${this.postcode}`
        );
        this.address = response.data.address;

        if (response.status !== 200) {
          throw new Error();
        }

        if (response.data.results === null) {
          this.errorMessage = '存在しない郵便番号です';
        }

        this.$emit(
          'address-found',
          response.data.results[0]['address1'] +
            response.data.results[0]['address2'] +
            response.data.results[0]['address3']
        );

        this.errorMessage = '';
      } catch (error) {
        this.errorMessage = '住所の取得に失敗しました';
      }
    },
  },
  watch: {
    postcode(newVal) {
      if (newVal.length === 7) {
        this.fetchAddress();
      }
    },
  },
  $emits: ['updated:modelValue'],
};
</script>

<style></style>
