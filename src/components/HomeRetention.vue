<template>
  <div class="home-retention">
    <h3>Subscription</h3>
    <img class="home-retention-icon" src="../assets/icon_dog_white.png" alt="dogIcon" />
    <p class="home-retention-bold">{{status}}</p>
    <img class="home-retention-icon" src="../assets/icon_calendar_white.png" alt="calendarIcon" />
    <p class="home-retention-bold">Next Delivery</p>
    <p class="home-retention-next-delivery">{{nextDelivery}}</p>
    <button class="btn-orange manage-btn">Manage Subscription</button>
    <button class="cancel-btn">Cancel Subscription</button>
  </div>
</template>

<script>
export default {
  name: "HomeRetention",
  props: {},
  data: () => {
    return {
      status: "Active",
      nextDelivery: "29th September 2020",
    };
  },
  methods: {},
};
</script>

<style>
.home-retention {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 5px;
  box-shadow: 0 0px 0px rgba(0, 0, 0, 0.3), 0 5px 11px rgba(0, 0, 0, 0.22);
  padding: 0 0 20px 0;
}

.home-retention-icon {
  width: 100px;
}

.manage-btn {
  width: 250px;
  box-shadow: none !important;
  margin-bottom: 10px !important;
}

.cancel-btn {
  width: 250px;
  border: solid #ee7623 1px;
  background-color: white;
  height: 30px;
  border-radius: 5px;
}
</style>
