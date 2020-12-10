<template>
  <div class="retention-component">
    <h2 class="cancel-header">Your subscription has been cancelled</h2>
    <img class="cancel-img" src="https://bellaandduke.imgix.net/2020/12/saddog.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=a116ba9859d18e77e2fccae9d06dc6eb" alt="Sad leaving dog">

    <a
      class="link"
      href="#"
      style="margin-top: 20px; font-size: 12px"
      @click="handleButton({ manageType: 'cancel' })"
      >Back</a
    >
  </div>
</template>

<script>
export default {
  name: "Cancelled",
  components: {},
  props: {},
  data: () => {
    return {};
  },
  methods: {
    handleButton(manageType) {
      manageType.subReason = this.cancelSubReason;
      this.$emit("manageSubmit", manageType);
    },
  },
};
</script>

<style scoped>
.cancel-img {
    height: 200px;
    width: 200px;
}
</style>
