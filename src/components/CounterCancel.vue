<template>
  <div id="counterCancel">
    <h2>{{ header }}</h2>
    <p>{{ message }}</p>
    <WistiaVideo v-if="videoLink" :videoLink="videoLink" />
    <h4 class="subHeader">{{ subHeader }}</h4>
    <div class="resolve-buttons">
      <div
        class="resolve-btn"
        v-for="(method, index) in resolveMethods"
        :key="index"
        @click="handleButton({manageType: method.resolveMethod})"
      >
        <img
          class="resolve-img"
          :src="require(`../assets/${method.icon}.png`)"
          :alt="method.icon"
        />
        <p class="resolve-btn-text">{{ method.text }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import WistiaVideo from "./BnDComponents/WistiaVideo";
export default {
  name: "CounterCancel",
  components: {
    WistiaVideo,
  },
  props: {
    reason: String,
  },
  data: () => {
    return {
      header: "",
      message: "",
      videoLink: "",
      subHeader: "",
      resolveMethods: "",
      resolveMethod: "",
    };
  },
  methods: {
    handleButton(manageType) {
      this.$emit("manageSubmit", manageType);
    },
    loadReason() {
      switch (this.reason) {
        case "notEatFood":
          this.header = `Lorem ipsum Scavenger Method`;
          this.message = `If your dog has become a little picky, then try the Scavenger 1-2-3 method. Developed by our in-house canine behaviourist, Caroline, it has a 98% success rate with fussy dogs:`;
          this.videoLink = `https://fast.wistia.com/embed/medias/rk0nnpgwi8`;
          this.subHeader = `Suscipit lobortis nisl ut aliquip`;
          this.resolveMethods = [{
              icon: "bowl",
              text: `Arrange a call with our in-houe behaviourist`,
              resolveMethod: "callResolve"
          }, {
              icon: "bowl",
              text: `Does your dog prefer dry food? Try our raw dry dog food`,
              resolveMethod: "tryDryResolve"
          }];
          break;
        default:
          this.header = this.message = this.videoLink = this.subHeader = "";
          break;
      }
    },
  },
  beforeMount() {
    this.loadReason();
  },
  watch: {
    reason: function () {
      this.loadReason();
    },
  },
};
</script>

<style scoped>
.subHeader {
    margin-bottom: 5px;
}
.resolve-buttons {
     display: flex;
  justify-content: space-evenly;
}

.resolve-btn {
  position: relative;
  border: 1px solid #00263a;
  border-radius: 5px;
  width: 135px;
  height: 135px;
  margin: 10px;
  cursor: pointer;
  box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
}

.resolve-btn:active {
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.2);
}

.resolve-btn-text {
  position: absolute;
  font-weight: 600;
  width: 110px;
  font-size: 10px;
  left: 0;
  right: 0;
  margin-top: 0;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 15px;
  bottom: 0;
}

.resolve-img {
  height: 80px;
}
</style>
