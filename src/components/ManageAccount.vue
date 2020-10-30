<template>
  <div class="retention-component">
    <h2>Your account</h2>
    <button class="bnd-btn orange-btn account-btn">History</button>
    <button class="bnd-btn orange-btn account-btn">Login & password</button>
    <button class="bnd-btn orange-btn account-btn">Your addresses</button>
    <button class="bnd-btn orange-btn account-btn">Your profile</button>
    <button class="bnd-btn green-btn cancel-btn" @click="handleButton({manageType: 'cancel'})">Cancel your account</button>
    <a
      class="link"
      href="#"
      style="margin-top: 20px; font-size: 12px"
      @click="handleButton({ manageType: 'example2'})"
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
