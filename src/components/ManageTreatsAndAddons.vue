<template>
  <div class="retention-component">
    <h2>Manage Treats & Addons</h2>
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
  name: "ManageTreatsAndAddons",
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
</style>
