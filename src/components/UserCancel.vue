<template>
  <div class="retention-component">
    <h2 class="cancel-header">Sorry to hear you're thinking of leaving us</h2>
    <p class="cancelling-help-text">
      Using only the highest quality, fresh ingredients we provide
      <b>[PET NAME]</b>
      with a natural & nutritionally balanced diet - designed to keep them
      healthy & happy.
      <br />
      <br />
      Tailored specifically, with all of the required vitamins & minerals, we
      have seen thousands of dogs thrive on our natural raw food.
    </p>
    <div class="cancel-cards">
      <div
        class="cancel-card"
        v-for="(cancelReasons, index) in cancelReasons"
        :key="index"
      >
        <img
          class="cancel-img"
          :src="require(`../assets/${cancelReasons.icon}.png`)"
          alt=""
        />
        <p class="cancel-card-text">{{ cancelReasons.text }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserCancel",
  components: {},
  props: {},
  data: () => {
    return {
      cancelReasons: [
        {
          icon: "icon_bowl_white_background",
          text: `It's too much food for my freezer`,
          order: Math.random(),
        },
        {
          icon: "icon_box_white_background",
          text: `I've moved to another food`,
          order: Math.random(),
        },
        {
          icon: "icon_price_white_background",
          text: `It's too expensive for me`,
          order: Math.random(),
        },
        {
          icon: "icon_dog_white_background",
          text: `My pet is not a fan of the food`,
          order: Math.random(),
        },
        {
          icon: "icon_low_tolerance_white_background",
          text: `I don't need it anymore`,
          order: Math.random(),
        },
        {
          icon: "icon_delivery_white_background",
          text: `I've experienced delivery issues`,
          order: Math.random(),
        },
      ],
    };
  },
  methods: {},
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
</style>
