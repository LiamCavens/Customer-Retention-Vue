<template>
  <div class="retention">
    <div class="retention-components">
      <UserCancel
        v-if="manageType === 'cancel'"
        :cancelReason="cancelReason"
        @manageSubmit="handleManage"
        @handleReason="handleReason"
      />
      <SecondChance
        v-if="manageType === 'secondChance'"
        :cancelReason="cancelReason"
        @manageSubmit="handleManage"
      />
      <UserFinalCancel
        v-if="manageType === 'finalCancel'"
        :cancelReason="cancelReason"
        @manageSubmit="handleManage"
      />
      <Cancelled
        v-if="manageType === 'cancelled'"
        :cancelReason="cancelReason"
        @manageSubmit="handleManage"
      />

      <!-- RESOLVE COMPONENTS -->
      <!-- <ResolveCall v-if="manageType === 'callResolve'" @manageSubmit="handleManage" /> -->
    </div>
  </div>
</template>

<script>
import Cancelled from "./Cancelled";
import SecondChance from "./SecondChance";
import UserCancel from "./UserCancel";
import UserFinalCancel from "./UserFinalCancel";

export default {
  name: "retentionv2",
  components: {
    Cancelled,
    SecondChance,
    UserCancel,

    UserFinalCancel,
  },
  props: {},
  data: () => {
    return {
      manageType: "cancel",
      cancelReason: "",
      cancelSubReason: "",
    };
  },
  methods: {
    handleManage(manageType) {
      this.manageType = manageType.manageType;
    },
    handleSubReason(subReason) {
      this.cancelSubReason = subReason;
    },
    handleReason(reason){
        this.cancelReason = reason;
    },
  },
};
</script>

<style>
.retention {
  background-color: white;
  width: 100%;
  display: flex;
  justify-content: center;
  /* flex: 1; */
}

.retention-components {
  margin: 10px;
  padding: 25px 10px;
  width: 350px;
  background-color: white;
  color: #00263a;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  position: relative;
  box-shadow: 0 19px 38px rgba(0, 0, 0, 0.3), 0 15px 12px rgba(0, 0, 0, 0.22);
}

.retention-component {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 5px;
  box-shadow: 0 0px 0px rgba(0, 0, 0, 0.3), 0 5px 11px rgba(0, 0, 0, 0.22);
  padding: 0 10px 20px 10px;
}
</style>
