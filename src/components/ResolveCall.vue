<template>
  <div id="resolveCall">
    <h2>Lorem ipsum call our behaviourist</h2>
    <p>
      Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper
      suscipit lobortis nisl ut aliquip ex ea commodo consequat.
    </p>
    <div class="call-calendar">
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
      <button class="bnd-btn green-btn" @click="handleResolve({ resolveType: 'requestCall' })">Request Call</button>
    </div>
    <a
      class="link"
      href="#"
      style="margin-top: 20px; font-size: 12px"
      @click="handleButton({ manageType: 'cancel' })"
      >Back</a
    >
  </div>
</template>

<script>
import { add, addBusinessDays } from "date-fns";
export default {
  name: "ResolveCall",
  components: {},
  props: {},
  data: () => {
    return {
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
  },
  watch: {
    requestCall: function () {
      this.callSelected = true;
    },
  },
};
</script>

<style scoped>
#resolveCall {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 10px;
}

.call-calendar {
  display: flex;
  flex-direction: column;
}

.call-calendar button {
  margin: 30px 10px 0;
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
