<template>
  <div class="row pt-3 text-center">
    <RsvpAttendance
      v-model:attendance="form.attendance"
      ref="attendance"
    ></RsvpAttendance>
  </div>
  <div class="row pt-3">
    <FormText
      v-model="form.last_name"
      name="last_name"
      label="姓"
      placeholder="石橋"
      :validation="['required']"
      ref="lastName"
    ></FormText>
    <FormText
      v-model="form.first_name"
      name="first_name"
      label="名"
      placeholder="さくら"
      :validation="['required']"
      ref="firstName"
    ></FormText>
  </div>
  <div class="row pt-3">
    <FormText
      v-model="form.last_name_kana"
      name="last_name_kana"
      label="セイ（カナ）"
      placeholder="イシバシ"
      :validation="['required', 'kana']"
      ref="lastNameKana"
    ></FormText>
    <FormText
      v-model="form.first_name_kana"
      name="first_name_kana"
      label="メイ（カナ）"
      placeholder="サクラ"
      :validation="['required', 'kana']"
      ref="firstNameKana"
    ></FormText>
  </div>
  <div class="row pt-3">
    <FormText
      v-model="form.email"
      name="email"
      label="メールアドレス（半角）"
      placeholder="sakurachan@example.com"
      :validation="['required', 'email']"
      ref="email"
    ></FormText>
  </div>
  <div class="row pt-3">
    <RsvpPostcode
      @address-found="handleAddressFound"
      v-model="form.postcode"
    ></RsvpPostcode>
  </div>
  <div class="row pt-3">
    <FormText
      v-model="form.address"
      name="address"
      label="住所"
      placeholder="北海道札幌市清田区０ー０ー０"
      :validation="['required', 'zenkaku']"
      ref="address"
    ></FormText>
  </div>
  <div class="row pt-3">
    <FormText
      v-model="form.building"
      name="building"
      label="建物・部屋番号（全角）"
      placeholder="トクトラスト美原"
      :validation="['zenkaku']"
      ref="building"
    ></FormText>
  </div>
  <div class="row pt-3">
    <FormText
      v-model="form.phone_number"
      name="phone_number"
      label="電話番号（ハイフンなし）"
      placeholder="00000000000"
      type="number"
      :validation="['required', 'hankaku-numeric']"
      ref="phoneNumber"
    ></FormText>
  </div>
  <div class="row pt-3">
    <FormCheck
      v-model:checked="form.is_input_allergic"
      label="アレルギーを入力しますか"
      name="is_input_allergic"
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
  <div class="row pt-3">
    <FormRadioGroup
      v-model="form.is_joining_after_party"
      label="二次会に参加します"
      name="is_joining_after_party"
      :options="afterPartyOptions"
      :validation="['required']"
      ref="isJoiningAfterParty"
    ></FormRadioGroup>
    <div class="row pt-2">
      <div
        class="col fs-7 ms-2 text-body-secondary"
        v-html="joiningAfterPartyMessage"
      ></div>
    </div>
  </div>

  <div class="row pt-3">
    <FormTextArea
      v-model="form.message"
      name="message"
      label="お祝いメッセージ等をご自由にご記入ください"
      rows="5"
      type="number"
    ></FormTextArea>
  </div>
</template>

<script>
import RsvpAttendance from './RsvpAttendance.vue';
import RsvpPostcode from './RsvpPostcode.vue';
import FormCheck from '../forms/FormCheck.vue';
import FormRadioGroup from '../forms/FormRadioGroup.vue';
import FormText from '../forms/FormText.vue';
import FormTextArea from '../forms/FormTextArea.vue';
export default {
  components: {
    RsvpAttendance,
    RsvpPostcode,
    FormCheck,
    FormRadioGroup,
    FormText,
    FormTextArea,
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
      form: {},
      joiningAfterPartyMessage: `会場は渋谷付近を想定しています
      おおよその人数を把握したいため ご回答お願いします
      詳細は幹事より別途連絡致します
      `,
    };
  },
  emits: ['update:form'],
  methods: {
    handleAddressFound(address) {
      this.form.address = address;
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

<style>
form {
  text-align: left;
}
</style>
