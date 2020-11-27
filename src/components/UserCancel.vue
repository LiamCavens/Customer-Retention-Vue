<template>
  <div class="retention-component">
    <h2 class="cancel-header">Help us understand why you are cancelling</h2>
    <!-- :fasIcon="['far', 'circle']" -->
    <BnDAccordion
      v-for="(cancel, index) in cancelReasons"
      :key="index"
      class="cancel-accordion"
      :heightProp="accordionHeight"
      @opened="currentAccordion = index"
      :showThis="index === currentAccordion"
    >
      <div slot="header">{{ cancel.text }}</div>
      <div class="subreasons">
        <p
          class="subreason"
          v-for="(subReason, index) in cancel.subReasons"
          :key="index"
          @click="handleSubReason(subReason.subReason, index)"
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

      <div ref="subReasonRef">
        <ResolveMethod
          v-if="resolveType"
          :reason="resolveType"
          @manageResolve="handleResolve"
        />
      </div>
    </BnDAccordion>

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
              solution: `Have you tried our Scavenger Method? Developed by Caroline, our in-house behaviourist, this method has a 95% success rate.`,
              solutionLinkText: "Learn More",
            },
            {
              subReasonText: "He/she prefers dry food",
              subReason: "preferDry",
              solution: `Have you tried our Scavenger Method? Developed by Caroline, our in-house behaviourist, this method has a 95% success rate.`,
              solutionLinkText: "Learn More",
            },
            {
              subReasonText: "Other",
              subReason: "callResolve",
              solution: `Maybe if you talk to one of our team we can help you with whatever your problem is.`,
              solutionLinkText: "Call us",
            },
          ],
        },
        {
          text: `I don't need the food`,
          cancelReason: `r2`,
          subReasons: [
            {
              subReasonText: "I don't need it anymore",
              subReason: "sr4",
              solution: `Though you might not need it now, if you will be needing orders soon, we offer you the choice to skip a number of deliveries so you dont forget and leave your dog hungry for Bella and Dukes!`,
              solutionLinkText: "Learn More",
            },
            {
              subReasonText: "It's too much food for freezer",
              subReason: "sr5",
              solution: `If you're struggling with freezer space, we can adjust the box size and frequency to adjust the amount of freezer space you have, if its a new freezer, we do have discount codes for you to use with our partnered sites.`,
              solutionLinkText: "Learn More",
            },
            {
              subReasonText: "I'm going on Holiday",
              subReason: "sr6",
              solution: `We can change the delivery address and dates to suit you and your dog better, or we can skip a delivery until you are back home.`,
              solutionLinkText: "Learn More",
            },
            {
              subReasonText: "I'm moving to another food",
              subReason: "sr15",
              solution: `We're sorry to hear this, are you able to tell us why you have decided to leave us? you can call one of our team to resolve any queries or you can let us know with a message next`,
              solutionLinkText: "Call us",
            },
          ],
        },
        {
          text: `Price`,
          cancelReason: `r3`,
          subReasons: [
            {
              subReasonText: "The order price is too much",
              subReason: "sr7",
              solution: `We do offer smaller box sizes which will lower your order price`,
              solutionLinkText: "Learn More",
            },
            {
              subReasonText: "The daily price is too high",
              subReason: "sr8",
              solution: `We offer larger box sizes, which come with a discount`,
              solutionLinkText: "Learn More",
            },
            {
              subReasonText: "I can't afford it",
              subReason: "sr9",
              solution: `If you would like to know why the prices of Bella and Duke are higher than average, we can have our customer team go through it with you, we offer the best nutrients to keep your pet healthy and living longer!`,
              solutionLinkText: "Call us",
            },
          ],
        },
        {
          text: `Convenience`,
          cancelReason: `r4`,
          subReasons: [
            {
              subReasonText: "I've experienced delivery issues",
              subReason: "sr10",
              solution: `You can call the team to let us know what has happened, as it may be out of our control but we would love to resolve the problem`,
              solutionLinkText: "Call us",
            },
            {
              subReasonText: "I don't want to have to defrost it",
              subReason: "sr11",
              solution: `Frozen ingredients & cold temp production locks in the nutrients, please click the link to learn more why this is best for your pets`,
              solutionLinkText: "Learn More",
            },
            {
              subReasonText: "I don't want a subscription",
              subReason: "sr12",
              solution: `You can manage your delivery schedule, payment method and order details, giving you complete control, click the link to modify your subscription`,
              solutionLinkText: "Manage Subscription",
            },
          ],
        },
        {
          text: `Dogs Health`,
          cancelReason: `r4`,
          subReasons: [
            {
              subReasonText: "My pet has an intolerance",
              subReason: "sr13",
              solution: `Many intolerances are a result of a processed diet, focused on the same protein day in day out. We belive that a varied diet resolves this, however you can adjust flavours here`,
              solutionLinkText: "Learn More",
            },
            {
              subReasonText: "My pet has died",
              subReason: "sr14",
              solution: `Losing a member of the family is never easy, but we are here to help in any way we can`,
              solutionLinkText: "",
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
      this.resetAccordionHeight();
    },
    handleSubReason(subReason, index) {
      this.resolveType = subReason;
      this.$emit("subReasonSubmit", subReason);
      this.resetAccordionHeight(index);
    },
    resetAccordionHeight(accordionIndex) {
      // It collapses the full accordion when changing radio
      accordionIndex = 0;
      let el = this.$refs.subReasonRef[accordionIndex];
      setTimeout(() => {
        this.accordionHeight = el.offsetHeight;
      }, 0);
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