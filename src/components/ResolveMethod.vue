<template>
  <div id="scav-method">
    <h2>{{ header }}</h2>
    <p>{{ message }}</p>

    <!-- <WistiaVideo v-if="reason === 'notEatFood'" /> -->
    <WistiaVideo />

    <div v-if="reason === 'dontNeedAnymore'" class="call-calendar">
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
    </div>

    <textarea
      v-if="reason === 'deliveryIssues' && !submittedToCS"
      class="cancel-box"
      name="cancelReasonText"
      id="cancelReasonText"
      v-model="cancelReasonText"
      cols="30"
      rows="10"
      placeholder="Can you tell us more about your issue?"
    ></textarea>

    <div v-if="submittedToCS">
      <p>
        Your issue has been passed on to our amazing customer service team, we
        will review this and forward it to our delivery courier
      </p>
    </div>

    <div style="width: 100%">
      <div v-if="ctaImage" class="image-div">
        <img class="cta-img" :class="{'img-resize': reason === 'movingFood' || reason === 'dontWantSubscription'}" :src="ctaImage" alt="methodImage" />
      </div>
      <a v-if="ctaLink" :href="ctaLink" target="_blank">
        <button v-if="ctaText" class="bnd-btn green-btn">
          {{ ctaText }}
        </button>
      </a>
      <button
        v-if="ctaText && !ctaLink"
        class="bnd-btn green-btn"
        @click="handleCta(ctaMethod)"
      >
        {{ ctaText }}
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
        <img class="resolve-img" :src="method.icon" />
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
      ctaImage: "",
      ctaText: "",
      ctaLink: "",
      ctaMethod: "",
      buttonsHeader: "",
      resolveMethods: "",
      resolveMethod: "",
      callSelected: false,
      submittedToCS: false,
      cancelReasonText: "",
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
    handleCta(ctaType) {
      if (ctaType === "cancelled") {
        this.handleButton({ manageType: ctaType });
      }
      if (ctaType === "cancel") {
        this.handleButton({ manageType: ctaType });
      }
      if (ctaType === "submitToCS") {
        this.submittedToCS = true;
        this.ctaText = "Return to portal";
        this.ctaMethod = "cancel";
      }
    },
    loadReason() {
      switch (this.reason) {
        case "notEatFood":
          this.header = `Scavenger Method`;
          this.message = `If your dog has become a little picky, then try the Scavenger 1-2-3 method. Developed by our in-house canine behaviourist, Caroline, it workes with 9/10 dogs:`;
          //   this.videoLink = `https://fast.wistia.com/embed/medias/rk0nnpgwi8`;
          this.buttonsHeader = `What about these issues?`;
          this.ctaImage = false;
          this.ctaLink = false;
          this.ctaText = false;
          this.ctaMethod = false;
          this.resolveMethods = [
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/phone.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=5aad099f1f86c91077d07f6155d44f81",
              text: `Arrange a call with our in-house behaviourist`,
              resolveMethod: "callResolve",
            },
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/bowl.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=421d2c8a910e2090c70705a5fe71f02d",
              text: `Does your dog prefer dry food? Try our raw dry dog food`,
              resolveMethod: "preferDry",
            },
          ];
          break;
        case "preferDry":
          this.header = `Raw Dry dog food`;
          this.message = `If your dog is used to kibble, then they may prefer a bit of crunch. We offer Raw Dry dog food, natural raw ingredients simply dried.`;
          this.videoLink = false;
          this.ctaImage =
            "https://bellaandduke.imgix.net/2020/12/BD-121.jpg?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=b41a0169ee42c8473fd53b84b6cf0ba2";
          this.ctaText = "Order now";
          this.ctaLink =
            "https://hello.bellaandduke.com/member/product-details/76";
          this.ctaMethod = false;
          this.buttonsHeader = `What about these issues?`;
          this.resolveMethods = [
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/phone.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=5aad099f1f86c91077d07f6155d44f81",
              text: `Arrange a call with our in-house behaviourist`,
              resolveMethod: "callResolve",
            },
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/clipboard.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=47d21217810e15c8440be3847f40a5a1",
              text: `try our effective Scavenger Method`,
              resolveMethod: "notEatFood",
            },
          ];
          break;
        case "callResolve":
          this.header = `Speak to our behaviourist`;
          this.message = `Some dogs need a little extra help. Arrange a call with our in-house canine behaviourist, Caroline.`;
          this.videoLink = false;
          this.ctaImage =
            "https://bellaandduke.imgix.net/2020/12/bd_caroline.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=74bad7bedb13e0e59deef757ea2056ff";
          this.ctaText = "Request call";
          this.ctaLink =
            "https://www.bellaandduke.com/dog-mealtime-advice-webinar/";
          this.ctaMethod = false;
          this.buttonsHeader = `What about these issues?`;
          this.resolveMethods = [
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/clipboard.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=47d21217810e15c8440be3847f40a5a1",
              text: `try our effective Scavenger Method`,
              resolveMethod: "notEatFood",
            },
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/bowl.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=421d2c8a910e2090c70705a5fe71f02d",
              text: `Does your dog prefer dry food? Try our raw dry dog food`,
              resolveMethod: "preferDry",
            },
          ];
          break;
        case "dontNeedAnymore":
          this.header = `Update Delivery Schedule`;
          this.message = `You have complete control over your deliveries.`;
          this.videoLink = false;
          this.ctaImage = false;
          this.ctaLink = false;
          this.ctaText = "Update";
          this.ctaMethod = false;
          this.buttonsHeader = `What about these issues?`;
          this.resolveMethods = [
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/box.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=42d9f71df61d60e0eb5df3332ad46652",
              text: `Adjust delivery size`,
              resolveMethod: "adjustDelivery",
            },
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/pin.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=0a9a0289da03677e71caa7ce99de834e",
              text: `Update my delivery address?`,
              resolveMethod: "newAddress",
            },
          ];
          break;
        case "adjustDelivery":
          this.header = `Adjust Delivery Size`;
          this.message = `If you have run out of freezer space, you can switch to a smaller box and adjust how often you recieve it.`;
          this.videoLink = false;
          this.ctaImage =
            "https://bellaandduke.imgix.net/2020/12/boxsizesg.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=e3d212552f307b1f1687a5285d73275f";
          this.ctaLink =
            "https://hello.bellaandduke.com/member/subscription-change-order-size";
          this.ctaText = "Change delivery size";
          this.ctaMethod = false;
          this.buttonsHeader = `What about these issues?`;
          this.resolveMethods = [
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/pin.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=0a9a0289da03677e71caa7ce99de834e",
              text: `Update my delivery address?`,
              resolveMethod: "newAddress",
            },
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/bowl.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=421d2c8a910e2090c70705a5fe71f02d",
              text: `Compare Bella & Duke with dry brands`,
              resolveMethod: "movingFood",
            },
          ];
          break;
        case "newAddress":
          this.header = `Are you taking the dog with you?`;
          this.message = `You can update your delivery address, to save taking the food with you.`;
          this.videoLink = false;
          this.ctaLink = "https://hello.bellaandduke.com/member/form-address";
          this.ctaImage = "https://bellaandduke.imgix.net/2020/12/holidaydog.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=8d113ee2b8f7ba57db940b6558a19709";
          this.ctaText = "Update delivery address";
          this.ctaMethod = false;
          this.buttonsHeader = `What about these issues?`;
          this.resolveMethods = [
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/bowl.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=421d2c8a910e2090c70705a5fe71f02d",
              text: `Moving to another food`,
              resolveMethod: "movingFood",
            },
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/calendar.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=42e32fe3a7d5e05ea3f44008ce2e98ff",
              text: `I don't need it anymore`,
              resolveMethod: "dontNeedAnymore",
            },
          ];
          break;
        case "movingFood":
          this.header = `Compare us with your new food`;
          this.message = `We believe our food is the best for your dog and we're willing to prove it!`;
          this.videoLink = false;
          this.ctaImage =
            "https://bellaandduke.imgix.net/2020/12/rawvdry.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=c7d8121615bfe3d9c5117e3c6372fdd6";
          this.ctaLink = "https://www.bellaandduke.com/how-it-works/";
          this.ctaText = "Compare now";
          this.ctaMethod = false;
          this.buttonsHeader = `What about these issues?`;
          this.resolveMethods = [
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/calendar.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=42e32fe3a7d5e05ea3f44008ce2e98ff",
              text: `I don't need it anymore`,
              resolveMethod: "dontNeedAnymore",
            },
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/clipboard.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=47d21217810e15c8440be3847f40a5a1",
              text: `Adjust delivery size`,
              resolveMethod: "adjustDelivery",
            },
          ];
          break;
        case "orderTooMuch":
          this.header = `Adjust Delivery Size`;
          this.message = `We offer smaller box sizes, which will lower your order price`;
          this.videoLink = false;
          this.ctaImage =
            "https://bellaandduke.imgix.net/2020/12/boxsizesg.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=e3d212552f307b1f1687a5285d73275f";
          this.ctaLink =
            "https://hello.bellaandduke.com/member/subscription-change-order-size";
          this.ctaText = "Change delivery size";
          this.ctaMethod = false;
          this.buttonsHeader = `What about these issues?`;
          this.resolveMethods = [
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/box.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=42d9f71df61d60e0eb5df3332ad46652",
              text: `Daily price too high`,
              resolveMethod: "dailyTooMuch",
            },
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/healthyheart.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=09fef542083dcefdf1b3908598a1ba1d",
              text: `I can't afford it`,
              resolveMethod: "cantAfford",
            },
          ];
          break;
        case "dailyTooMuch":
          this.header = `Adjust Delivery Size`;
          this.message = `We offer larger box sizes, which come with a discount`;
          this.videoLink = false;
          this.ctaImage =
            "https://bellaandduke.imgix.net/2020/12/boxsizeso.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=2fd97f25610ae56bf0da5275a16de3ef";
          this.ctaText = "Change delivery size";
          this.ctaLink =
            "https://hello.bellaandduke.com/member/subscription-change-order-size";
          this.ctaMethod = false;
          this.buttonsHeader = `What about these issues?`;
          this.resolveMethods = [
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/box.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=42d9f71df61d60e0eb5df3332ad46652",
              text: `Order price too high`,
              resolveMethod: "orderTooMuch",
            },
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/healthyheart.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=09fef542083dcefdf1b3908598a1ba1d",
              text: `I can't afford it`,
              resolveMethod: "cantAfford",
            },
          ];
          break;
        case "cantAfford":
          this.header = `Quality food for healthy pets`;
          this.message = `All of our meals are designed to support your pet's health. They are made from the highest quslity, 100% natural ingredients, carefully sourced from British & Irish farms.`;
          this.videoLink = false;
          this.ctaImage = "https://bellaandduke.imgix.net/2020/12/chickenbox.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=2611ee9fb274001fbf79e088e74bbd9f";
          this.ctaText = "Find out more";
          this.ctaMethod = false;

          this.ctaLink = "https://www.bellaandduke.com/nutrition/";
          this.buttonsHeader = `What about these issues?`;
          this.resolveMethods = [
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/box.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=42d9f71df61d60e0eb5df3332ad46652",
              text: `Daily price too high`,
              resolveMethod: "dailyTooMuch",
            },
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/bowl.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=421d2c8a910e2090c70705a5fe71f02d",
              text: `Order price too high`,
              resolveMethod: "dailyTooMuch",
            },
          ];
          break;
        case "deliveryIssues":
          this.header = `Let us know what happened`;
          this.message = `We will take this up with our couriers so we can improve our service`;
          this.videoLink = false;
          this.ctaImage = false;
          this.ctaText = "Submit";
          this.ctaLink = false;
          this.ctaMethod = "submitToCS";
          this.buttonsHeader = `What about these issues?`;
          this.resolveMethods = [
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/frozen.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=9ecc7544621cec132d2e10c67e9d3bd6",
              text: `I don't want to defrost`,
              resolveMethod: "notDefrost",
            },
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/clipboard.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=47d21217810e15c8440be3847f40a5a1",
              text: `I dont want a subscription`,
              resolveMethod: "dontWantSubscription",
            },
          ];
          break;
        case "notDefrost":
          this.header = `Frozen to lock in nutrients`;
          this.message = `Our natural ingredients are simple mixed together and frozen to lock in nutrients. This removes the need for nasty preservatives.`;
          this.videoLink = false;
          this.ctaImage = "https://bellaandduke.imgix.net/2020/12/freezer.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=9ec205ca3d41db1fb940cb184d678284";
          this.ctaText = "Help with defrosting";
          this.ctaMethod = false;
          this.ctaLink =
            "https://help.bellaandduke.com/hc/en-gb/articles/360015560657-Defrosting-your-food";
          this.buttonsHeader = `What about these issues?`;
          this.resolveMethods = [
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/clipboard.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=47d21217810e15c8440be3847f40a5a1",
              text: `I dont want a subscription`,
              resolveMethod: "dontWantSubscription",
            },
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/van.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=8cf718fa6656cf3467dc9dddd850697d",
              text: `Delivery issues`,
              resolveMethod: "deliveryIssues",
            },
          ];
          break;
        case "dontWantSubscription":
          this.header = `Take control of your customer portal`;
          this.message = `Auto-deliveries mean you won't run out of food. However, if you want to manage this manually you can adjust delivery schedule, payment method and order details, in your customer portal.`;
          this.videoLink = false;
          this.ctaImage =
            "https://bellaandduke.imgix.net/2020/12/checklist.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=027edaafdb8dc09feba4938db708c935";
          this.ctaText = "Modify subscription";
          this.ctaMethod = false;
          this.ctaLink =
            "https://hello.bellaandduke.com/member/subscription-changes";
          this.buttonsHeader = `What about these issues?`;
          this.resolveMethods = [
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/frozen.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=9ecc7544621cec132d2e10c67e9d3bd6",
              text: `I don't want to defrost`,
              resolveMethod: "notDefrost",
            },
            {
              icon:
                "https://bellaandduke.imgix.net/2020/12/van.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=8cf718fa6656cf3467dc9dddd850697d",
              text: `Delivery issues`,
              resolveMethod: "deliveryIssues",
            },
          ];
          break;
        case "intolerance":
          this.header = `Customise your order`;
          this.message = `Many intolerances are a result of a processed diet, focused on the same protein day in day out. We belive that a varied diet resolves this, however you can adjust flavours or change range here`;
          this.videoLink = false;
          this.ctaImage =
            "https://bellaandduke.imgix.net/2020/12/range.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=7b52179bd368175131f3918a02aedfb4";
          this.ctaText = "Modify subscription";
          this.ctaMethod = false;
          this.ctaLink =
            "https://hello.bellaandduke.com/member/subscription-changes";
          this.buttonsHeader = '';
          this.resolveMethods = false;
          break;
        case "petPassed":
          this.header = `Sorry for your loss`;
          this.message = `Losing a member of the family is never easy, but we are here to help in any way we can.`;
          this.videoLink = false;
          this.ctaImage = "https://bellaandduke.imgix.net/2020/12/saddog.png?auto=compress%2Cformat&ixlib=php-3.3.0&q=60&s=a116ba9859d18e77e2fccae9d06dc6eb";
          this.ctaText = "Cancel";
          this.ctaLink = false;
          this.ctaMethod = "cancelled";
          this.buttonsHeader = "";
          this.resolveMethods = false;
          break;
        default:
          this.header = this.message = this.videoLink = this.buttonsHeader = this.resolveMethods =
            "";
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

.image-div {
  height: 190px;
}

.cta-img {
  height: 190px;
  border-radius: 50%;
}

.img-resize {
    border-radius: 0 !important;
    width: 100%;
}

.cancel-box {
  font-family: Montserrat;
  padding: 10px;
  margin: 10px;
}

.cta-link {
  color: #fff;
  text-decoration: none;
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
