<template>
  <div class="retention-component">
    <h2>Your account</h2>
    <button class="btn-green account-btn">History</button>
    <button class="btn-green account-btn">Login & password</button>
    <button class="btn-green account-btn">Your addresses</button>
    <button class="btn-green account-btn">Your profile</button>
    <button class="btn-green cancel-btn">Cancel your account</button>
    <a
      class="link"
      href="#"
      style="margin-top: 20px; font-size: 12px"
      @click="handleButton({ manageType: 'example2', retentionStage: 0 })"
      >Back</a
    >
  </div>
</template>

<script>
export default {
  name: "ManageAccount",
  props: {},
  data: () => {
    return {};
  },
  methods: {
    handleButton(manageType) {
      this.$emit("manageSubmit", manageType);
    },
  },
};
</script>

<style scoped>
.account-btn{
    width: 275px;
    font-weight: 600;
}

.cancel-btn{
    background-color: #fff;
    color: #789904;
    width: 275px;
    font-weight: 600;
}
</style>
