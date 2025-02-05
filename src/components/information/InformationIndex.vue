<template>
  <section>
    <div class="container">
      <div class="pt-5">
        <h2 class="p-4">INFORMATION</h2>
      </div>
      <div class="pb-5" id="time-info">
        <div class="row">
          <div class="col">
            <div class="fs-4">日時</div>
            <div class="fs-1">2025.04.26 (Sat)</div>
          </div>
        </div>
        <div class="row">
          <div class="col">
            <div class="fs-5">挙式</div>
            <div class="fs-1">15:30</div>
          </div>
          <div class="col">
            <div class="fs-5">受付</div>
            <div class="fs-1">15:50</div>
          </div>
          <div class="col">
            <div class="fs-5">披露宴</div>
            <div class="fs-1">16:15</div>
          </div>
        </div>
        <hr />
        <div class="row">
          <div class="col" v-html="assembly"></div>
        </div>
      </div>
      <div class="bg-white m-1">
        <h4 class="p-4">会場情報</h4>
        <div class="text-start">
          <div class="row p-2 m-2 border-top">
            <div class="col-4">url</div>
            <div class="col">
              <a
                href="https://catstreet.trunk-hotel.com/wedding/"
                target="_blank"
              >
                https://catstreet.trunk-hotel.com/wedding/
              </a>
            </div>
          </div>
          <div class="row p-2 m-2 border-top">
            <div class="col-4">場所</div>
            <div class="col" v-html="place"></div>
          </div>
          <div class="row p-2 m-2 border-top">
            <div class="col-4">アクセス</div>
            <div class="col" v-html="address"></div>
          </div>
          <div class="row p-2 m-2">
            <div class="col">
              <iframe
                src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3241.5157214714886!2d139.70143687589643!3d35.66430143090354!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x60188ca6f5129f93%3A0x46c4cd2fba503530!2sTRUNK(HOTEL)%20CAT%20STREET!5e0!3m2!1sja!2sjp!4v1736054372320!5m2!1sja!2sjp"
                width="100%"
                height="300"
                style="border: 0"
                allowfullscreen=""
                loading="lazy"
                referrerpolicy="no-referrer-when-downgrade"
              ></iframe>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      place: `TRUNK(HOTEL)
                3F SORANIWA
                `,
      address: `〒150-0001
                東京都渋谷区神宮前5-31
                TEL:03-5766-3200`,
      assembly: `当日は15時15分までにお越しくださいますよう
                よろしくお願い申し上げます
      `,
    };
  },
};
</script>

<style></style>
