<template>
  <hr />
  <div class="pt-3 ps-3 pe-3 visible">
    <div class="row pt-3 visible">
      <FormText
        v-model="form.last_name"
        :name="'last_name' + index"
        label="姓"
        placeholder="石原"
        :visible="true"
        :validation="['required']"
        ref="lastName"
      ></FormText>
      <FormText
        v-model="form.first_name"
        :name="'first_name' + index"
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
        :name="'last_name_kana' + index"
        label="セイ（カナ）"
        placeholder="イシハラ"
        :visible="true"
        :validation="['required', 'kana']"
        ref="lastNameKana"
      ></FormText>
      <FormText
        v-model="form.first_name_kana"
        :name="'first_name_kana' + index"
        label="メイ（カナ）"
        placeholder="サトミ"
        :visible="true"
        :validation="['required', 'kana']"
        ref="firstNameKana"
      ></FormText>
    </div>
    <div class="row pt-3 visible">
      <FormCheck
        v-model:checked="form.is_input_allergic"
        label="アレルギーを入力しますか"
        :name="'is_input_allergic' + index"
        :visible="true"
        @change="isCheck($event.target.checked)"
      ></FormCheck>
    </div>
    <div v-if="isInputAllergic" class="toggle-area visible">
      <div class="m-3 p-3 bg-white visible">
        <p v-html="allergicMessage"></p>
        <a href="https://caneat.jp/45/event/9ce3be81" target="_blank">
          https://caneat.jp/45/event/9ce3be81
        </a>
      </div>
    </div>
    <div class="row pt-3 visible">
      <FormRadioGroup
        v-model="normalizedKey"
        label="二次会に参加します"
        :name="'is_joining_after_party' + index"
        :visible="true"
        :options="afterPartyOptionsWithIndex"
        :validation="['required']"
        ref="isJoiningAfterParty"
      ></FormRadioGroup>
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
import FormRadioGroup from '../forms/FormRadioGroup.vue';

export default {
  components: {
    FormText,
    FormCheck,
    FormRadioGroup,
  },
  data() {
    return {
      afterPartyOptions: {
        joining: 'はい',
        nonJoining: 'いいえ',
      },
      isInputAllergic: false,
      allergicMessage: `お食事に制限がある方は
      下記URLサイトからご回答をお願いします`,
      form: {
        is_joining_after_party: '', // 初期値を追加
      },
    };
  },
  emits: ['remove', 'update:form'],
  props: {
    index: Number,
  },
  computed: {
    // index を追加した後の選択肢
    afterPartyOptionsWithIndex() {
      const options = {};
      for (const [key, value] of Object.entries(this.afterPartyOptions)) {
        options[`${key}_${this.index}`] = value;
      }
      return options;
    },
    // index 付きの key をもとに、index を省いた key に変換
    normalizedKey: {
      get() {
        return this.form.is_joining_after_party
          ? this.form.is_joining_after_party + `_${this.index}`
          : '';
      },
      set(value) {
        if (value) {
          this.form.is_joining_after_party = value.replace(
            `_${this.index}`,
            ''
          );
          this.$emit('update:form', this.form);
        }
      },
    },
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
