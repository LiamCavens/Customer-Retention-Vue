<template>
  <div class="retention-component">
    <h2 class="cancel-header">Your subscription has been cancelled</h2>
    <pre>
 
   ,_____ ,
  ,._ ,_. 7\
 j `-'     /
 |o_, o    \
.`_y_`-,'   !
|/   `, `._ `-,
|_     \   _.'*\
  >--,-'`-'*_*'``---.
  |\_* _*'-'         '
 /    `               \
 \.         _ .       /
  '`._     /   )     /
   \  |`-,-|  /c-'7 /
    ) \ (_,| |   / (_
   ((_/   ((_;)  \_)))
    </pre>

    <a
      class="link"
      href="#"
      style="margin-top: 20px; font-size: 12px"
      @click="handleButton({ manageType: 'secondChance' })"
      >Back</a
    >
  </div>
</template>

<script>
export default {
  name: "Cancelled",
  components: {},
  props: {},
  data: () => {
    return {};
  },
  methods: {
    handleButton(manageType) {
      manageType.subReason = this.cancelSubReason;
      this.$emit("manageSubmit", manageType);
    },
  },
};
</script>

<style scoped>
</style>
