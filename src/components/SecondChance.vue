<template>
  <div class="retention-component">
    <h2 class="cancel-header">We hate to see you go</h2>
    <p class="cancel-message">
      Mark & Tony are gutted that you are thinking of cancelling. Not only will
      you will stop recieving scheduled deliveries of natural, healthy raw food,
      but you will also lose access to exclusive perks like Bella & Duke
      RAWARDS.
    </p>
    <button
      class="bnd-btn green-btn button"
      @click="handleButton({ manageType: 'cancel' })"
    >
      Return to portal
    </button>
    <button
      class="bnd-btn white-btn button"
      @click="handleButton({ manageType: 'finalCancel' })"
    >
      Continue to cancellation
    </button>
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
  name: "SecondChance",
  components: {},
  props: {},
  data: () => {
    return {
      userInputReason: "",
    };
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
.retention-component {
  padding-left: 30px;
  padding-right: 30px;
}

.cancel-header {
  margin-bottom: 5px;
}

.bnd-btn {
  width: 100%;
}

button:disabled,
button[disabled] {
  opacity: 0.5;
}
</style>

