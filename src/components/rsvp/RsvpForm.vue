<template>
  <form class="pt-4" @submit.prevent="submitForm">
    <div class="pt-3 ps-3 pe-3">
      <RsvpFormGroups @update:form="updateForm"></RsvpFormGroups>
    </div>
    <div class="row mt-3">
      <button type="button" class="btn btn-light">
        お連れ様を追加する<svg
          xmlns="http://www.w3.org/2000/svg"
          width="16"
          height="16"
          fill="currentColor"
          class="bi bi-person-plus-fill"
          viewBox="0 0 16 16"
        >
          <path
            d="M1 14s-1 0-1-1 1-4 6-4 6 3 6 4-1 1-1 1zm5-6a3 3 0 1 0 0-6 3 3 0 0 0 0 6"
          />
          <path
            fill-rule="evenodd"
            d="M13.5 5a.5.5 0 0 1 .5.5V7h1.5a.5.5 0 0 1 0 1H14v1.5a.5.5 0 0 1-1 0V8h-1.5a.5.5 0 0 1 0-1H13V5.5a.5.5 0 0 1 .5-.5"
          />
        </svg>
      </button>
    </div>
    <div class="row mt-3">
      <button type="submit" class="btn btn-bridal">送信する</button>
    </div>
  </form>
  <p v-if="successMessage">{{ successMessage }}</p>
</template>

<script>
import RsvpFormGroups from './RsvpFormGroups.vue';
export default {
  components: {
    RsvpFormGroups,
  },
  data() {
    return {
      isInputAllergic: false,
      foundAddress: '',
      allergicMessage: `お食事に制限がある方は
      下記URLサイトからご回答をお願いします`,
      form: {},
      successMessage: '',
    };
  },
  methods: {
    handleAddressFound(address) {
      this.foundAddress = address;
    },
    isCheck(check) {
      this.isInputAllergic = check === true;
    },
    updateForm(newForm) {
      this.form = newForm;
    },
    async submitForm() {
      const url =
        'https://script.google.com/macros/s/AKfycbwqj2Twap84n30PBSHyscnL4VV0n6eIJaeycUJp5utaR8mokWqs0v52Bbzsk4UVIvjI/exec'; // デプロイしたURLを入力
      try {
        const response = await fetch(url, {
          method: 'POST',
          headers: {
            'Content-Type': 'text/plain',
          },
          mode: 'cors', // CORS を有効にする
          body: JSON.stringify(this.form),
        });
        const result = await response.json();
        if (result.success) {
          this.successMessage = '送信が完了しました！';
          this.formData = { message: '' };
        } else {
          this.successMessage = '送信に失敗しました。';
        }
      } catch (error) {
        this.successMessage = 'エラーが発生しました。';
      }
    },
  },
};
</script>

<style>
form {
  text-align: left;
}
</style>
