<template>
  <section id="rsvp">
    <div class="container">
      <div class="bg-white p-3" style="--bs-bg-opacity: 0.5">
        <div class="text-center pt-5">
          <h2>RSVP</h2>
        </div>
        <RsvpMessage :deadline="deadline"></RsvpMessage>
        <RsvpForm></RsvpForm>
      </div>
    </div>
  </section>
</template>

<script>
import RsvpForm from './RsvpForm.vue';
import RsvpMessage from './RsvpMessage.vue';

export default {
  components: {
    RsvpForm,
    RsvpMessage,
  },
  props: {
    deadline: {
      required: true,
      type: String,
    },
  },
};
</script>

<style scoped></style>
