<template>
  <div class="col">
    <label for="postcode" class="form-label">郵便番号（ハイフンなし）</label>
    <div class="row">
      <div class="col-9">
        <input
          v-if="this.errorMessage !== ''"
          v-model="postcode"
          class="form-control is-invalid"
          type="text"
          name="postcode"
          id="postcode"
          placeholder="0000000"
        />
        <input
          v-else
          v-model="postcode"
          class="form-control"
          type="text"
          name="postcode"
          id="postcode"
          placeholder="0000000"
        />
        <div
          v-if="this.errorMessage !== ''"
          class="invalid-feedback text-break"
        >
          {{ this.errorMessage }}
        </div>
      </div>
      <div class="col-2">
        <button @click.prevent="fetchAddress" class="btn btn-light">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="16"
            height="16"
            fill="currentColor"
            class="bi bi-search"
            viewBox="0 0 16 16"
          >
            <path
              d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"
            />
          </svg>
        </button>
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
      try {
        const response = await axios.get(
          `http://localhost:8000/api/address/search?postcode=${this.postcode}`
        );

        if ('address' in response.data) {
          this.$emit('address-found', response.data.address);
          this.errorMessage = '';
        }

        if ('errors' in response.data) {
          this.errorMessage = response.data.errors.postcode[0];
        }
      } catch (error) {
        console.log(error);
        this.errorMessage = 'APIエラーが発生しました。';
      }
    },
  },
};
</script>

<style></style>
