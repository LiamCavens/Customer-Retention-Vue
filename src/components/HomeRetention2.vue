<template>
  <div class="retention-component">
    <!-- <h3 class="home-retention-bold">Subscription</h3>
    <img class="home-retention-icon" src="../assets/icon_calendar_white.png" alt="calendarIcon" /> -->
    <p class="home-retention-bold">Your Next Delivery</p>
    <p class="home-retention-text">
      {{ nextDelivery | moment("dddd, Do MMMM YYYY") }}
    </p>
    <p class="home-retention-small">Payment Date : XXth December</p>
    <!-- <button class="green-btn retention-btn">Manage account</button> -->
    <BnDAccordion v-for="(accordion, index) in manageAccordions" :key="index" class="retention-accordion" theme="bottomBorder">
      <div slot="header">{{accordion.manageHeader}}</div>
      <p class="accordion-text">
        {{accordion.manageText}}
      </p>
      <button class="bnd-btn green-btn accordion-btn" :class="{'orange-btn' : !accordion.active}" @click="handleButton({manageType: accordion.manageType})">
        {{accordion.manageButtonText}}
      </button>
    </BnDAccordion>

    <a class="link" href="#" style="margin-top: 20px; font-size: 12px" @click="handleButton({manageType: 'example1'})">See Example 1</a>
  </div>
</template>

<script>
import BnDAccordion from "./BnDComponents/BnDAccordion";
export default {
  name: "HomeRetention2",
  components: {
    BnDAccordion,
  },
  props: {},
  data: () => {
    return {
      status: "Active",
      joinDate: "13th March 2020",
      nextDelivery: "",
      manageAccordions: [
        {
          manageHeader: `Manage deliveries`,
          manageText: `Change your delivery dates, cancel or modify your next delivery or
        change your schedule of deliveries`,
          manageType: `deliveries`,
          manageButtonText: `Change Deliveries`,
          retentionStage: 1
        },
        {
          manageHeader: `Manage pets & food`,
          manageText: `Manage your pet food including including or excluding proteins. Add or
        change pets and add or remove them from the food plan.`,
          manageType: `petsAndFood`,
          manageButtonText: `Change pets or food`,
          retentionStage: 1
        },
        {
          manageHeader: `Manage account`,
          manageText: `Manage your password, contact, payment or delivery details or the status
        of your account.`,
          manageType: `account`,
          manageButtonText: `Change account details`,
          retentionStage: 1,
          active: true
        },
        {
          manageHeader: `Manage treats & addons`,
          manageText: `Add treats and add-ons to your deliveries or as an hoc order..`,
          manageType: `treatsAndAddon`,
          manageButtonText: `Change Treats and addons`,
          retentionStage: 1
        },
        {
          manageHeader: `Help`,
          manageText: `Let us help you with anything`,
          manageType: `help`,
          manageButtonText: `Talk to us`,
          retentionStage: 1
        },
      ],
    };
  },
  methods: {
    handleButton(manageType) {
      this.$emit("manageSubmit", manageType);
    },
    randomDate(startDate, endDate) {
      return new Date(
        startDate.getTime() +
          Math.random() * (endDate.getTime() - startDate.getTime())
      );
    },
  },
  mounted() {
    this.nextDelivery = this.randomDate(new Date(), new Date(2021, 12, 30));
  },
};
</script>

<style scoped>
.home-retention-icon {
  width: 100px;
}

.home-retention-bold {
  font-weight: 600;
  font-size: 24px;
  margin: 20px 0 0 0;
}

.home-retention-text {
  margin: 8px;
}

.home-retention-small {
  font-size: 12px;
}

.retention-btn {
  width: 250px;
  font-weight: 600;
  background-color: goldenrod !important;
}

.retention-accordion {
  width: 250px;
}

.accordion-text {
  font-size: 12px;
  margin: 0;
  text-align: left;
}
</style>

