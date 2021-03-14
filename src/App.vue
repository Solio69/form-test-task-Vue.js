<template>
  <div id="app">
    <Form @checkForm="outDataInForm" v-if="!showSuccess"></Form>
    <Success v-else></Success>
  </div>
</template>

<script>
import Form from "@/components/Form.vue";
import Success from "@/components/Success.vue";
export default {
  components: { Form, Success },
  name: "App",
  data() {
    return {
      showSuccess: false,
    };
  },
  methods: {
    outDataInForm(formData) {
      console.log(formData);
      this.showSuccess = true;
    },
  },
};
</script>

<style scoped></style>
