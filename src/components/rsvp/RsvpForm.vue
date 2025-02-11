<template>
  <form class="pt-4" @submit.prevent="submitForm">
    <div class="pt-3 ps-3 pe-3">
      <RsvpFormGroups
        ref="formGroups"
        @update:form="updateForm"
      ></RsvpFormGroups>
    </div>

    <RsvpCompanion
      v-for="(companion, index) in companions"
      :key="index"
      :index="index"
      @update:form="(newForm) => updateCompanionForm(newForm, index)"
      @remove="removeCompanion(index)"
      ref="companions"
    ></RsvpCompanion>

    <div class="row mt-3">
      <button
        type="button"
        class="btn btn-light"
        @click="addCompanion"
        :disabled="companions.length >= 2 || isSubmitting"
      >
        お連れ様を追加する
      </button>
    </div>

    <div class="row mt-3">
      <button
        type="submit"
        class="btn btn-bridal"
        :disabled="isSubmitCompleted ? isSubmitCompleted : isSubmitting"
      >
        <span v-if="isSubmitting">送信中...</span>
        <span v-else>送信する</span>
      </button>
    </div>
  </form>
  <p v-if="submitMessage">{{ submitMessage }}</p>
</template>

<script>
import RsvpFormGroups from './RsvpFormGroups.vue';
import RsvpCompanion from './RsvpCompanion.vue';

export default {
  components: {
    RsvpFormGroups,
    RsvpCompanion,
  },
  data() {
    return {
      companions: [],
      form: {
        self: {},
        companions: [],
      },
      isSubmitting: false,
      isSubmitCompleted: false,
      submitMessage: '',
    };
  },
  methods: {
    addCompanion() {
      if (this.companions.length < 2) {
        this.companions.push({});
      }
    },
    removeCompanion(index) {
      this.companions.splice(index, 1);
      this.form.companions.splice(index, 1);
    },
    updateForm(newForm) {
      this.form.self = newForm;
    },
    updateCompanionForm(newForm, index) {
      this.form.companions[index] = newForm;
    },
    async submitForm() {
      if (this.isSubmitting) return;
      this.isSubmitting = true;
      this.submitMessage = '';

      const url =
        'https://script.google.com/macros/s/AKfycbwqj2Twap84n30PBSHyscnL4VV0n6eIJaeycUJp5utaR8mokWqs0v52Bbzsk4UVIvjI/exec';

      let validateCompanions = true;

      if (Array.isArray(this.$refs.companions)) {
        this.$refs.companions.forEach((ref) => {
          let thisError = ref.validateAll();
          validateCompanions =
            validateCompanions === false ? validateCompanions : thisError;
        });
      }

      if (!this.$refs.formGroups.validateAll() || !validateCompanions) {
        this.isSubmitting = false;
        return;
      }

      try {
        const response = await fetch(url, {
          method: 'POST',
          headers: { 'Content-Type': 'text/plain' },
          mode: 'cors',
          body: JSON.stringify(this.form),
        });

        const result = await response.json();
        if (result.success) {
          this.submitMessage = `送信が完了しました`;
          this.isSubmitCompleted = true;
        } else {
          this.submitMessage = '送信に失敗しました';
        }
      } catch (error) {
        this.submitMessage = 'エラーが発生しました';
      } finally {
        this.isSubmitting = false;
      }
    },
  },
};
</script>

<style>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s ease-in-out;
}

.modal.visible {
  opacity: 1;
  pointer-events: auto;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 8px;
  text-align: center;
}
</style>
