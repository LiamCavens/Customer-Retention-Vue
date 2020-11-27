<template>
  <div class="retention-component">
    <h2 class="cancel-header">Everyone deserves a second chance</h2>
    <p class="cancel-message">
      We are confident that a natural raw diet is the best choice for <b>{dogName}</b>. With a bit of encouragement, we are sure that they will be happier
      and healthier continuing with Bella & Duke, so we can offer you an
      exclusive one-off discount on your next box:
    </p>
    <button
      class="bnd-btn green-btn button"
      @click="handleButton({ manageType: 'example2' })"
    >
      Try again with 30% off
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

