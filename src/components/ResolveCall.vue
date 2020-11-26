<template>
  <div>
    <h2>Lorem ipsum call our behaviourist</h2>
    <p>
      Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper
      suscipit lobortis nisl ut aliquip ex ea commodo consequat.
    </p>
    <div class="delivery-calendar">
      <!-- <v-calendar v-if="!loading && !datePicking" :attributes="attributes" /> -->
      <!-- <v-date-picker v-if="!loading && datePicking" v-model="delivery1" is-inline /> -->
      <v-date-picker
        id="date-picker"
        v-model="delivery1"
        :select-attribute="selectAttribute"
        :disabled-dates="[
          { weekdays: [1, 7] },
          { start: null, end: new Date() },
        ]"
        is-inline
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "ResolveCall",
  components: {},
  props: {},
  data: () => {
    return {};
  },
  methods: {},
};
</script>

<style>
</style>
