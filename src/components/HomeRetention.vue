<template>
  <div class="home-retention">
    <h3 class="home-retention-bold">Subscription</h3>
    <img class="home-retention-icon" src="../assets/icon_dog_white.png" alt="dogIcon" />
    <p class="home-retention-bold">{{status}}</p>
    <p class="home-retention-text">Added {{joinDate}}</p>
    <img class="home-retention-icon" src="../assets/icon_calendar_white.png" alt="calendarIcon" />
    <p class="home-retention-bold">Next Delivery</p>
    <p class="home-retention-text">{{nextDelivery}}</p>
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
      joinDate: "13th March 2020",
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

.home-retention-bold {
  font-family: Montserrat-bold;
  font-size: 24px;
  margin: 20px 0 0 0;
}

.home-retention-text {
  margin: 8px;
}

.manage-btn {
  width: 250px;
  box-shadow: none !important;
  margin-bottom: 10px !important;
}

.cancel-btn {
  font-family: Montserrat;
  width: 250px;
  color: #00263a;
  border: solid #ee7623 1px;
  background-color: white;
  height: 30px;
  border-radius: 5px;
  padding: 2px;
  border: solid #d3671b 1px;
  cursor: pointer;
  text-align: center;
}

.cancel-btn:hover {
  background-image: -webkit-linear-gradient(top, #fff, #f0f0f0);
  background-image: -moz-linear-gradient(top, #fff, #f0f0f0);
  background-image: -ms-linear-gradient(top, #fff, #f0f0f0);
  background-image: -o-linear-gradient(top, #fff, #f0f0f0);
  background-image: linear-gradient(to bottom, #fff, #f0f0f0);
}
</style>
