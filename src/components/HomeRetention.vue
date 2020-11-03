<template>
  <div class="retention-component">
    <!-- <h3 class="home-retention-bold">Subscription</h3>
    <img class="home-retention-icon" src="../assets/icon_calendar_white.png" alt="calendarIcon" /> -->
    <p class="home-retention-bold">Your Next Delivery</p>
    <p class="home-retention-text">
      {{ nextDelivery | moment("dddd, Do MMMM YYYY") }}
    </p>
    <p class="home-retention-small">Payment Date : XXth December</p>
    <!-- <button class="green-btn bnd-btn retention-btn">Manage account</button> -->
    <button class="bnd-btn retention-btn" disabled>Manage deliveries</button>
    <button class="bnd-btn retention-btn" disabled>Manage pets & food</button>
    <button class="bnd-btn retention-btn" disabled>Manage account</button>
    <button
      class="green-btn bnd-btn retention-btn"
      @click="handleButton({ manageType: 'example2' })"
    >
      See Example 2.
    </button>
  </div>
</template>

<script>
export default {
  name: "HomeRetention",
  props: {},
  data: () => {
    return {
      status: "Active",
      joinDate: "13th March 2020",
      nextDelivery: "",
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
}
</style>
