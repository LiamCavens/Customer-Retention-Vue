<template>
  <div id="scav-method">
    <h2>{{ header }}</h2>
    <p>{{ message }}</p>

    <WistiaVideo v-if="reason === 'notEatFood'" videoLink="https://fast.wistia.com/embed/medias/rk0nnpgwi8" />

    <div v-if="reason === 'callResolve'" class="call-calendar">
      <v-date-picker
        id="date-picker"
        v-model="requestCall"
        :select-attribute="selectAttribute"
        :theme="calendarTheme"
        :disabled-dates="[
          { weekdays: [1, 7] },
          { start: null, end: new Date() },
        ]"
        is-inline
      />
      <button
        class="bnd-btn green-btn"
        @click="handleResolve({ resolveType: 'requestCall' })"
      >
        Request Call
      </button>
    </div>

    <div v-if="reason === 'preferDry'">
        <img class="dry-food-img" src="../assets/chickhearts.jpg" alt="dry food">
              <button
        class="bnd-btn green-btn"
        @click="handleResolve({ resolveType: 'switchToRaw' })"
      >
        Switch to Dry Raw
      </button>
    </div>

    <h4 class="buttonsHeader">{{ buttonsHeader }}</h4>
    <div class="resolve-buttons">
      <div
        class="resolve-btn"
        v-for="(method, index) in resolveMethods"
        :key="index"
        @click="handleResolve({ resolveType: method.resolveMethod })"
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
import { add, addBusinessDays } from "date-fns";

import WistiaVideo from "./BnDComponents/WistiaVideo";

export default {
  name: "ResolveMethod",
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
      buttonsHeader: "",
      resolveMethods: "",
      resolveMethod: "",
            callSelected: false,
      requestCall: addBusinessDays(new Date(), 1),
      selectAttribute: {
        highlight: {
          color: "green",
          class: "bella-duke-green",
        },
        popover: {
          label: "First Delivery",
        },
        contentStyle: {
          color: "#00263a",
        },
        dates: add(new Date(), { weeks: 1 }),
      },
      calendarTheme: {
        isDark: true,
        container: { dark: "vc-bnd-navy" },
        header: { dark: "calendar-header" },
        weekdays: {
          dark: "white-days",
        },
      },
    };
  },
  methods: {
    handleButton(manageType) {
      this.$emit("manageSubmit", manageType);
    },
    handleResolve(resolveType) {
      this.$emit("manageResolve", resolveType);
    },
    loadReason() {
      switch (this.reason) {
        case "notEatFood":
          this.header = `Lorem ipsum Scavenger Method`;
          this.message = `If your dog has become a little picky, then try the Scavenger 1-2-3 method. Developed by our in-house canine behaviourist, Caroline, it has a 98% success rate with fussy dogs:`;
          this.videoLink = `https://fast.wistia.com/embed/medias/rk0nnpgwi8`;
          this.buttonsHeader = `Suscipit lobortis nisl ut aliquip`;
          this.resolveMethods = [
            {
              icon: "phone",
              text: `Arrange a call with our in-house behaviourist`,
              resolveMethod: "callResolve",
            },
            {
              icon: "bowl",
              text: `Does your dog prefer dry food? Try our raw dry dog food`,
              resolveMethod: "preferDry",
            },
          ];
          break;
        case "preferDry":
          this.header = `Lorem ipsum dolor sit Raw Dry dog food`;
          this.message = `Lorem ipsum dolor sitLorem ipsum dolor sitLorem ipsum dolor sitLorem ipsum dolor sitLorem ipsum dolor sitLorem ipsum dolor sitLorem ipsum dolor sit:`;
        //   this.videoLink = false;
          this.buttonsHeader = `Suscipit lobortis nisl ut aliquip`;
          this.resolveMethods = [
            {
              icon: "phone",
              text: `Arrange a call with our in-house behaviourist`,
              resolveMethod: "callResolve",
            },
            {
              icon: "clipboard",
              text: `try our 98% effective Scavenger Method`,
              resolveMethod: "notEatFood",
            },
          ];
          break;
        case "callResolve":
          this.header = `Lorem ipsum dolor sit our behaviourist`;
          this.message = `Lorem ipsum dolor sitLorem ipsum dolor sitLorem ipsum dolor sitLorem ipsum dolor sitLorem ipsum dolor sitLorem ipsum dolor sitLorem ipsum dolor sit:`;
        //   this.videoLink = false;
          this.buttonsHeader = `Suscipit lobortis nisl ut aliquip`;
          this.resolveMethods = [
            {
              icon: "clipboard",
              text: `try our 98% effective Scavenger Method`,
              resolveMethod: "notEatFood",
            },
            {
              icon: "bowl",
              text: `Does your dog prefer dry food? Try our raw dry dog food`,
              resolveMethod: "preferDry",
            },
          ];
          break;
        default:
          this.header = this.message = this.videoLink = this.buttonsHeader = "";
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
#scav-method {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}
.buttonsHeader {
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
  width: 120px;
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

.dry-food-img {
    height: 190px;
    border-radius: 50%;
}

.green-btn {
    width: 100%;
    margin: 30px 0 10px;
}
</style>

<style>
.bella-duke-green {
  background-color: #789904 !important;
}
.vc-bnd-navy {
  color: #fff !important;
  background-color: #00263a !important;
  border-radius: 5% !important;
}

.calendar-header {
  font-family: Montserrat;
}

.white-days {
  font-family: Montserrat;
  color: #fff !important;
}
</style>
