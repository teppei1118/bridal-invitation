<template>
  <form class="pt-4">
    <div class="pt-3 ps-3 pe-3">
      <div class="row pt-3 text-center">
        <div class="col">
          <input
            class="attendance-input"
            type="radio"
            name="attendance"
            id="attendance-attend"
            value="1"
          />
          <label for="attendance-attend" class="form-label">出席</label>
        </div>
        <div class="col">
          <input
            class="attendance-input"
            type="radio"
            name="attendance"
            id="attendance-absence"
            value="2"
          />
          <label for="attendance-absence" class="form-label">欠席</label>
        </div>
      </div>
      <div class="row pt-3">
        <FormText name="last_name" label="姓" placeholder="石橋"></FormText>
        <FormText name="first_name" label="名" placeholder="さくら"></FormText>
      </div>
      <div class="row pt-3">
        <FormText
          name="last_name_kana"
          label="セイ（カナ）"
          placeholder="イシバシ"
        ></FormText>
        <FormText
          name="first_name_kana"
          label="メイ（カナ）"
          placeholder="サクラ"
        ></FormText>
      </div>
      <div class="row pt-3">
        <RsvpPostcode @address-found="handleAddressFound"></RsvpPostcode>
      </div>
      <div class="row pt-3">
        <FormText
          name="address"
          label="住所"
          placeholder="北海道札幌市清田区O-O-O"
          :value="foundAddress"
        ></FormText>
      </div>
      <div class="row pt-3">
        <FormText
          name="building"
          label="建物・部屋番号（全角）"
          placeholder="トクトラスト美原"
        ></FormText>
      </div>
      <div class="row pt-3">
        <FormText
          name="phone-number"
          label="電話番号（ハイフンなし）"
          placeholder="00000000000"
          type="number"
        ></FormText>
      </div>
    </div>
  </form>
</template>

<script>
import RsvpPostcode from './RsvpPostcode.vue';
import FormText from '../forms/FormText.vue';
export default {
  components: {
    RsvpPostcode,
    FormText,
  },
  data() {
    return {
      foundAddress: '',
    };
  },
  methods: {
    handleAddressFound(address) {
      this.foundAddress = address;
    },
  },
};
</script>

<style>
form {
  text-align: left;
}
</style>
