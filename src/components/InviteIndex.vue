<template>
  <MainIndex></MainIndex>
  <CountdownIndex :deadline="deadline"></CountdownIndex>
  <IntroductionIndex></IntroductionIndex>
  <HostIndex></HostIndex>
  <!--    スライドショー-->
  <InformationIndex></InformationIndex>
  <RsvpIndex :deadline="deadline"></RsvpIndex>
</template>

<script>
import CountdownIndex from './countdown/CountdownIndex.vue';
import HostIndex from './host/HostIndex.vue';
import InformationIndex from './information/InformationIndex.vue';
import IntroductionIndex from './introduction/IntroductionIndex.vue';
import MainIndex from './main/MainIndex.vue';
import RsvpIndex from './rsvp/RsvpIndex.vue';

export default {
  components: {
    CountdownIndex,
    HostIndex,
    InformationIndex,
    IntroductionIndex,
    MainIndex,
    RsvpIndex,
  },
  props: {
    deadline: {
      required: true,
      type: String,
    },
  },
};
</script>

<style></style>
