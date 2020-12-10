<template>
  <div class="retention-component">
    <h2 class="cancel-header">Help us understand why you are cancelling</h2>
    <!-- :fasIcon="['far', 'circle']" -->
    <BnDAccordion
      v-for="(cancel, accordionIndex) in cancelReasons"
      :key="accordionIndex"
      class="cancel-accordion"
      :heightProp="accordionHeight"
      @opened="
        resetReason(accordionIndex, currentAccordion);
        currentAccordion = accordionIndex;
      "
      :showThis="accordionIndex === currentAccordion"
    >
      <div slot="header">{{ cancel.text }}</div>
      <div ref="subReasonRef">
        <div class="subreasons">
          <p
            class="subreason"
            v-for="(subReason, subIndex) in cancel.subReasons"
            :key="subIndex"
            @click="handleReason(subReason.subReason, accordionIndex)"
          >
            {{ subReason.subReasonText }}
            <span
              class="checkedSub filled-circle"
              v-if="subReason.subReason === resolveType"
            ></span>
            <span
              class="checkedSub hollow-circle"
              v-if="subReason.subReason != resolveType"
            ></span>
          </p>
        </div>

        <div>
          <ResolveMethod
            v-if="resolveType"
            :reason="resolveType"
            @manageResolve="handleResolve"
            @manageSubmit="handleButton"
          />
        </div>
      </div>
    </BnDAccordion>

    <button
      class="bnd-btn white-btn button"
      @click="handleButton({ manageType: 'example2' })"
    >
      Return to portal
    </button>

    <button
      class="bnd-btn white-btn button"
      @click="handleButton({ manageType: 'secondChance' })"
      :disabled="!resolveType"
    >
      Continue Cancellation
    </button>

    <a
      class="link"
      href="#"
      style="margin-top: 20px; font-size: 12px"
      @click="handleButton({ manageType: 'example2' })"
      >Back</a
    >
  </div>
</template>

<script>
import BnDAccordion from "./BnDComponents/BnDAccordion";
import ResolveMethod from "./ResolveMethod";

export default {
  name: "UserCancel",
  components: {
    BnDAccordion,
    ResolveMethod,
  },
  props: {},
  data: () => {
    return {
      cancelReason: "",
      cancelSubReason: "",
      accordionHeight: 0,
      currentAccordion: -1,
      resolveType: "",
      cancelReasons: [
        {
          text: `My pet is a fussy eater`,
          cancelReason: `fussy`,
          subReasons: [
            {
              subReasonText: "He/She wouldn't eat the food",
              subReason: "notEatFood",
            },
            {
              subReasonText: "He/she prefers dry food",
              subReason: "preferDry",
            },
            {
              subReasonText: "Other",
              subReason: "callResolve",
            },
          ],
        },
        {
          text: `I don't need the food`,
          cancelReason: `dontNeedFood`,
          subReasons: [
            {
              subReasonText: "I don't need it anymore",
              subReason: "dontNeedAnymore",
            },
            {
              subReasonText: "It's too much food for freezer",
              subReason: "adjustDelivery",
            },
            {
              subReasonText: "I'm going on Holiday",
              subReason: "newAddress",
            },
            {
              subReasonText: "I'm moving to another food",
              subReason: "movingFood",
            },
          ],
        },
        {
          text: `Price`,
          cancelReason: `price`,
          subReasons: [
            {
              subReasonText: "The order price is too much",
              subReason: "orderTooMuch",
            },
            {
              subReasonText: "The daily price is too high",
              subReason: "dailyTooMuch",
            },
            {
              subReasonText: "I can't afford it",
              subReason: "cantAfford",
            },
          ],
        },
        {
          text: `Convenience`,
          cancelReason: `convenience`,
          subReasons: [
            {
              subReasonText: "I've experienced delivery issues",
              subReason: "deliveryIssues",
            },
            {
              subReasonText: "I don't want to have to defrost it",
              subReason: "notDefrost",
            },
            {
              subReasonText: "I don't want a subscription",
              subReason: "dontWantSubscription",
            },
          ],
        },
        {
          text: `Dogs Health`,
          cancelReason: `dogHealth`,
          subReasons: [
            {
              subReasonText: "My pet has an intolerance",
              subReason: "intolerance",
            },
            {
              subReasonText: "My pet has died",
              subReason: "petPassed",
            },
          ],
        },
      ],
    };
  },
  methods: {
    handleButton(manageType) {
      manageType.subReason = this.cancelSubReason;
      this.$emit("manageSubmit", manageType);
    },
    handleResolve(resolveType) {
      this.resolveType = resolveType.resolveType;
      this.resetAccordionHeight(this.currentAccordion);
    },
    handleReason(subReason, accordionIndex) {
      this.resolveType = subReason;
      this.$emit("handleReason", subReason);
      this.resetAccordionHeight(accordionIndex);
    },
    resetReason(accordionIndex, previousAccordion) {
      if (accordionIndex != previousAccordion) {
        this.resolveType = this.cancelReason = this.cancelSubReason = "";
        // Get subreasons and get their height
        let subReasonEl = this.$refs.subReasonRef[accordionIndex];
        this.accordionHeight = subReasonEl.offsetHeight;
        setTimeout(() => {
          let subReasonEl = this.$refs.subReasonRef[accordionIndex];
          this.accordionHeight = subReasonEl.offsetHeight;
        }, 100);
      }
    },
    resetAccordionHeight(newIndex) {
      if (!newIndex) newIndex = 0;
      setTimeout(() => {
        let el = this.$refs.subReasonRef[newIndex];
        this.accordionHeight = el.offsetHeight;
      }, 100);
    },
  },
};
</script>

<style scoped>
.cancel-header {
  margin-bottom: 25px;
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

.subreasons {
  display: flex;
  flex-direction: column;
  align-items: start;
  margin-left: 15px;
}
.subreason {
  cursor: pointer;
  margin: 10px;
  width: 100%;
  display: flex;
  font-size: 12px;
  margin: 4px 0px;
  position: relative;
}

.checkedSub {
  position: absolute;
  right: 20px;
}

.cancel-solution {
  background-color: #789904;
  width: 100%;
}

.solution-text {
  color: #fff;
  font-size: 12px;
  text-align: left;
  padding: 5px;
}
.solution-link-p {
  text-align: left;
  padding: 0 0 5px 5px;
  font-size: 14px;
}

.solution-link {
  color: #fff;
}

.filled-circle {
  border-radius: 50%;
  height: 10px;
  width: 10px;
  background-color: #789904;
  box-shadow: inset 0px 0px 0px 2px #fff;
  border: 2px solid #00263a;
}

.hollow-circle {
  border-radius: 50%;
  height: 10px;
  width: 10px;
  background-color: #fff;
  border: 2px solid #00263a;
}

.cancel-accordion {
  width: 300px;
}

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

.cancel-radio:hover .check {
  border: 3px solid #789904;
}
</style>