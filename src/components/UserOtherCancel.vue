<template>
  <div class="retention-component">
    <h2 class="cancel-header">Let us know why you are cancelling</h2>
    <BnDAccordion
      v-for="(cancel, index) in cancelReasons"
      :key="index"
      class="cancel-accordion"
      theme="noBorder"
      :fasIcon="['far', 'circle']"
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
            v-if="subReason.subReason === cancelSubReason"
          ></span>
          <span
            class="checkedSub hollow-circle"
            v-if="subReason.subReason != cancelSubReason"
          ></span>
        </p>
        <div
          v-for="(subReason, index) in cancel.subReasons"
          :key="`${index}-subreason`"
          ref="subReasonRef"
        >
          <div
            class="cancel-solution"
            v-if="subReason.subReason === cancelSubReason"
          >
            <p class="solution-text">{{ subReason.solution }}</p>
            <p class="solution-link-p">
              <a class="solution-link" href="#">{{
                subReason.solutionLinkText
              }}</a>
            </p>
          </div>
        </div>
      </div>
    </BnDAccordion>

    <button
      class="bnd-btn white-btn button"
      @click="handleButton({ manageType: 'finalCancel' })"
      :disabled="!cancelReason"
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
export default {
  name: "UserOtherCancel",
  components: {
    BnDAccordion,
  },
  props: {},
  data: () => {
    return {
      cancelReason: "",
      cancelSubReason: "",
      accordionHeight: 0,
      currentAccordion: -1,
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
              subReason: "otherFussy",
              solution: `Maybe if you talk to one of our team we can help you with whatever your problem is.`,
              solutionLinkText: "Call us",
            },
          ],
        },
        {
          text: `Reason 2`,
          cancelReason: `r2`,
          subReasons: [
            {
              subReasonText: "Sub-Reason 4",
              subReason: "sr4",
              solution: `Something is going to go in here that is actually useful to the customer, if this does not help you, please contact Sholto as its his problem now`,
              solutionLinkText: "Learn More",
            },
            {
              subReasonText: "Sub-Reason 5",
              subReason: "sr5",
              solution: `Something is going to go in here that is actually useful to the customer, if this does not help you, please contact Sholto as its his problem now`,
              solutionLinkText: "Learn More",
            },
            {
              subReasonText: "Sub-Reason 6",
              subReason: "sr6",
              solution: `Something is going to go in here that is actually useful to the customer, if this does not help you, please contact Sholto as its his problem now`,
              solutionLinkText: "Learn More",
            },
          ],
        },
        {
          text: `Reason 3`,
          cancelReason: `r3`,
          subReasons: [
            {
              subReasonText: "Sub-Reason 7",
              subReason: "sr7",
              solution: `Something is going to go in here that is actually useful to the customer, if this does not help you, please contact Sholto as its his problem now`,
              solutionLinkText: "Learn More",
            },
            {
              subReasonText: "Sub-Reason 8",
              subReason: "sr8",
              solution: `Something is going to go in here that is actually useful to the customer, if this does not help you, please contact Sholto as its his problem now`,
              solutionLinkText: "Learn More",
            },
            {
              subReasonText: "Sub-Reason 9",
              subReason: "sr9",
              solution: `Something is going to go in here that is actually useful to the customer, if this does not help you, please contact Sholto as its his problem now`,
              solutionLinkText: "Learn More",
            },
          ],
        },
        {
          text: `Reason 4`,
          cancelReason: `r4`,
          subReasons: [
            {
              subReasonText: "Sub-Reason 10",
              subReason: "sr10",
              solution: `Something is going to go in here that is actually useful to the customer, if this does not help you, please contact Sholto as its his problem now`,
              solutionLinkText: "Learn More",
            },
            {
              subReasonText: "Sub-Reason 11",
              subReason: "sr11",
              solution: `Something is going to go in here that is actually useful to the customer, if this does not help you, please contact Sholto as its his problem now`,
              solutionLinkText: "Learn More",
            },
            {
              subReasonText: "Sub-Reason 12",
              subReason: "sr12",
              solution: `Something is going to go in here that is actually useful to the customer, if this does not help you, please contact Sholto as its his problem now`,
              solutionLinkText: "Learn More",
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
    handleSubReason(subReason, subIndex) {
      this.cancelSubReason = subReason;
      let el = this.$refs.subReasonRef[subIndex];
        this.$emit('subReasonSubmit', subReason)
      //   this.handleButton({ manageType: "userCancelInput" });
      setTimeout(() => {
        this.accordionHeight = el.offsetHeight;
      }, 0);
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
  font-size: 14px;
  margin: 8px 0px;
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