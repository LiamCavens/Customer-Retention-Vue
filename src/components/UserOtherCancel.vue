<template>
  <div class="retention-component">
    <h2 class="cancel-header">Let us know why you are cancelling</h2>
    <ul class="cancel-list">
      <li
        class="cancel-radio"
        v-for="(reason, index) in cancelReasons"
        :key="index"
      >
        <input
          type="radio"
          :id="reason.cancelReason"
          :name="reason.cancelReason"
          :value="reason.cancelReason"
          v-model="cancelReason"
        />
        <label :for="reason.cancelReason">{{ reason.text }}</label>
        <div class="check"></div>
      </li>
    </ul>
    <button
      class="bnd-btn white-btn button"
      @click="handleButton({ manageType: 'finalCancel' })"
      :disabled="!cancelReason"
    >
      Continue Cancellation
    </button>
  </div>
</template>

<script>
export default {
  name: "UserOtherCancel",
  components: {},
  props: {},
  data: () => {
    return {
      cancelReason: "",
      cancelReasons: [
        {
          text: `Reason 1`,
          cancelReason: `r1`,
        },
        {
          text: `Reason 2`,
          cancelReason: `r2`,
        },
        {
          text: `Reason 3`,
          cancelReason: `r3`,
        },
        {
          text: `Reason 4`,
          cancelReason: `r4`,
        },
      ],
    };
  },
  methods: {
    handleButton(manageType) {
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

.bnd-btn {
  width: 300px;
}

button:disabled,
button[disabled] {
  opacity: 0.5;
}
</style>


<style scoped>
.cancel-list {
  list-style-type: none;
  padding: 0;
  /* display: flex; */
}
.cancel-radio input[type="radio"] {
  position: absolute;
  visibility: hidden;
}

.cancel-radio label {
  display: flex;
  justify-content: start;
  position: relative;
  padding: 10px 50px 10px 0;
  font-size: 14px;
  z-index: 9;
  cursor: pointer;
  transition: all 0.25s linear;
}

.cancel-radio {
  position: relative;
}

.check {
  display: block;
  position: absolute;
  border: 3px solid #aaaaaa;
  border-radius: 100%;
  height: 12px;
  width: 12px;
  top: 12px;
  right: 0;
  z-index: 5;
  transition: border 0.25s linear;
  -webkit-transition: border 0.25s linear;
}

.check::before {
  display: block;
  position: absolute;
  content: "";
  border-radius: 100%;
  height: 8px;
  width: 8px;
  top: 2px;
  left: 2px;
  margin: auto;
  transition: background 0.25s linear;
  -webkit-transition: background 0.25s linear;
}

input[type="radio"]:checked ~ .check {
  border: 3px solid #789904;
}

input[type="radio"]:checked ~ .check::before {
  background: #789904;
}

/* input[type="radio"]:checked ~ label {
  color: #789904;
} */

.cancel-radio:hover .check {
  border: 3px solid #789904;
}
</style>