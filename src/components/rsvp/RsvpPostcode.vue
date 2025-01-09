<template>
  <div class="col">
    <label for="postcode" class="form-label">郵便番号（ハイフンなし）</label>
    <div class="row">
      <div class="col">
        <input
          v-if="this.errorMessage !== ''"
          v-model="postcode"
          class="form-control is-invalid"
          type="text"
          name="postcode"
          id="postcode"
          placeholder="0000000"
          maxlength="7"
          @input="fetchAddress"
        />
        <input
          v-else
          v-model="postcode"
          class="form-control"
          type="text"
          name="postcode"
          id="postcode"
          placeholder="0000000"
          maxlength="7"
          @input="fetchAddress"
        />
        <div
          v-if="this.errorMessage !== ''"
          class="invalid-feedback text-break visible"
        >
          {{ this.errorMessage }}
        </div>
      </div>
    </div>
    <div v-if="this.errorMessage !== ''" class="invalid-feedback">
      {{ this.errorMessage }}
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
    };
  },
  methods: {
    async fetchAddress() {
      if (this.postcode.length === 7) {
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

          console.log(response.data.results[0]);
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
      }
    },
  },
};
</script>

<style></style>
