<template>
  <div class="retention-component">
    <h2 class="cancel-header">We'd love to know why</h2>
    <textarea class="cancel-box" name="cancelReason" id="cancelReason" v-model="userInputReason" cols="36" rows="10" placeholder="Type in the box why you are leaving Bella & Duke"></textarea>
    <button
      class="bnd-btn white-btn button"
      @click="handleButton({ manageType: 'finalCancel' })"
      :disabled="!userInputReason"
    >
      Continue Cancellation
    </button>
  </div>
</template>

<script>
export default {
  name: "UserCancelInput",
  components: {},
  props: {},
  data: () => {
    return {
        userInputReason: ''
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
.cancel-header {
  margin-bottom: 5px;
}

.cancel-cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
}

.cancel-card {
  position: relative;
  border: 1px solid #00263a;
  border-radius: 5px;
  width: 135px;
  height: 135px;
  margin: 10px;
  cursor: pointer;
}

.cancel-card-text {
  position: absolute;
  width: 110px;
  font-size: 12px;
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
  bottom: 0;
}

.cancelling-help-text {
  margin: 5px;
  padding: 0 20px;
  font-size: 14px;
}

.cancel-img {
  height: 100px;
}

.cancel-link {
  color: #789904;
  text-decoration: underline;
}

.cancel-box {
    font-family: Montserrat;
}

.bnd-btn {
  width: 300px;
}

button:disabled,
button[disabled] {
  opacity: 0.5;
}
</style>

