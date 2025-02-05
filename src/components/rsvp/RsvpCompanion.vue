<template>
  <hr />
  <div class="pt-3 ps-3 pe-3 visible">
    <div class="row pt-3 visible">
      <FormText
        v-model="form.last_name"
        name="last_name"
        label="姓"
        placeholder="石原"
        :visible="true"
        :validation="['required']"
        ref="lastName"
      ></FormText>
      <FormText
        v-model="form.first_name"
        name="first_name"
        label="名"
        placeholder="さとみ"
        :visible="true"
        :validation="['required']"
        ref="firstName"
      ></FormText>
    </div>
    <div class="row pt-3 visible">
      <FormText
        v-model="form.last_name_kana"
        name="last_name_kana"
        label="セイ（カナ）"
        placeholder="イシハラ"
        :visible="true"
        :validation="['required', 'kana']"
        ref="lastNameKana"
      ></FormText>
      <FormText
        v-model="form.first_name_kana"
        name="first_name_kana"
        label="メイ（カナ）"
        placeholder="サトミ"
        :visible="true"
        :validation="['required', 'email']"
        ref="firstNameKana"
      ></FormText>
    </div>
    <div class="row pt-3 visible">
      <FormCheck
        v-model:checked="form.is_input_allergic"
        label="アレルギーを入力しますか"
        name="is_input_allergic"
        :visible="true"
        @change="isCheck($event.target.checked)"
      ></FormCheck>
    </div>
    <div v-if="isInputAllergic" class="toggle-area visible">
      <div class="m-3 p-3 bg-white visible">
        <p v-html="allergicMessage"></p>
        <a href="https://caneat.jp/45/event/9ce3be81" target="_blank"
          >https://caneat.jp/45/event/9ce3be81</a
        >
      </div>
    </div>
  </div>

  <div class="row mt-3 visible">
    <button type="button btn" class="btn btn-danger" @click="removeCompanion">
      お連れ様を削除する
    </button>
  </div>
</template>

<script>
import FormText from '../forms/FormText';
import FormCheck from '../forms/FormCheck.vue';
export default {
  components: {
    FormText,
    FormCheck,
  },
  data() {
    return {
      isInputAllergic: false,
      allergicMessage: `お食事に制限がある方は
      下記URLサイトからご回答をお願いします`,
      form: {},
    };
  },
  emits: ['remove', 'update:form'],
  props: {
    index: Number,
  },
  methods: {
    removeCompanion() {
      this.$emit('remove', this.index);
    },
    isCheck(check) {
      this.isInputAllergic = check === true;
    },
    validateAll() {
      let isError = false;
      Object.values(this.$refs)
        .flat()
        .forEach((ref) => {
          if (ref.validate) {
            let thisError = ref.validate() === false;
            isError = isError ? isError : thisError;
          }
        });

      return isError === false;
    },
  },
  watch: {
    form: {
      handler(newForm) {
        this.$emit('update:form', newForm);
      },
      deep: true,
    },
  },
};
</script>
