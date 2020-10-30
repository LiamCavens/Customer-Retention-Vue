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
      <UserCancel
        v-if="manageType === 'cancel'"
        :cancelReason="cancelReason"
        @manageSubmit="handleManage"
      />
      <UserOtherCancel
        v-if="manageType === 'cancelOther'"
        :cancelReason="cancelReason"
        @manageSubmit="handleManage"
      />
      <UserFinalCancel
        v-if="manageType === 'finalCancel'"
        :cancelReason="cancelReason"
        @manageSumbit="handleManage"
      />

      <Cancelled
        v-if="manageType === 'cancelled'"
        :cancelReason="cancelReason"
        @manageSumbit="handleManage"
      />
    </div>
  </div>
</template>

<script>
import Cancelled from "./Cancelled";
import UserCancel from "./UserCancel";
import UserOtherCancel from "./UserOtherCancel";
import UserFinalCancel from "./UserFinalCancel";
import HomeRetention from "./HomeRetention";
import HomeRetention2 from "./HomeRetention2";
import ManageAccount from "./ManageAccount";
import ManageDelivery from "./ManageDelivery";
import ManagePetsAndFood from "./ManagePetsAndFood";
import ManageTreatsAndAddons from "./ManageTreatsAndAddons";

export default {
  name: "retentionv2",
  components: {
    Cancelled,
    UserCancel,
    UserOtherCancel,
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
      manageType: "cancelOther",
      cancelReason: "",
    };
  },
  methods: {
    handleManage(manageType) {
      console.log("Liam: manageType");
      console.log(manageType);
      this.manageType = manageType.manageType;
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

.slide-fade-enter-active {
  transition: all 0.8s ease;
  transition-delay: 0.4s;
}
.slide-fade-leave-active {
  transition: all 0.3s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-fade-enter {
  transform: translateY(100px);
  opacity: 0;
}

.slide-fade-leave-to {
  transform: translateY(-50px);
  opacity: 0;
}

.help-transition-leave-active,
.help-transition-enter-active {
  transition: opacity 0.5s ease;
}

.help-transition-enter,
.help-transition-leave-to {
  opacity: 0;
}

.help-transition-enter-to,
.help-transition-leave {
  opacity: 1;
}
</style>
