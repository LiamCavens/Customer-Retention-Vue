<template>
  <div class="retention">
    <div class="retention-components">
      <HomeRetention
        v-if="manageType === 'example1'"
        @manageSubmit="handleManage"
      />
      <HomeRetention2
        v-if="manageType === 'example2'"
        @manageSubmit="handleManage"
      />
      <ManageAccount
        v-if="manageType === 'account'"
        @manageSubmit="handleManage"
      />
      <ManageDelivery
        v-if="manageType === 'deliveries'"
        @manageSubmit="handleManage"
      />
      <ManagePetsAndFood
        v-if="manageType === 'petsAndFood'"
        @manageSubmit="handleManage"
      />
      <ManageTreatsAndAddons
        v-if="manageType === 'treatsAndAddons'"
        @manageSubmit="handleManage"
      />
      <UserCancel2
        v-if="manageType === 'cancel2'"
        :cancelReason="cancelReason"
        @manageSubmit="handleManage"
      />
      <UserCancel
        v-if="manageType === 'cancel'"
        :cancelReason="cancelReason"
        @manageSubmit="handleManage"
        @subReasonSubmit="handleSubReason"
      />
      <UserCancelInput
        v-if="manageType === 'userCancelInput'"
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
      <ResolveCall v-if="manageType === 'callResolve'" />
    </div>
  </div>
</template>

<script>
import Cancelled from "./Cancelled";
import UserCancel2 from "./UserCancel2";
import UserCancelInput from "./UserCancelInput";
import UserCancel from "./UserCancel";
import UserFinalCancel from "./UserFinalCancel";
import HomeRetention from "./HomeRetention";
import HomeRetention2 from "./HomeRetention2";
import ManageAccount from "./ManageAccount";
import ManageDelivery from "./ManageDelivery";
import ManagePetsAndFood from "./ManagePetsAndFood";
import ManageTreatsAndAddons from "./ManageTreatsAndAddons";

// RESOLVE COMPONENETS

import ResolveCall from "./ResolveCall";

export default {
  name: "retentionv2",
  components: {
    Cancelled,
    UserCancel2,
    UserCancelInput,
    UserCancel,
    ResolveCall,
    UserFinalCancel,
    HomeRetention,
    HomeRetention2,
    ManageAccount,
    ManageDelivery,
    ManagePetsAndFood,
    ManageTreatsAndAddons,
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
  padding: 0 0 20px 0;
}
</style>
