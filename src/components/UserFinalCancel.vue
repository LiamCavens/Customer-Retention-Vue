<template>
  <div class="retention-component">
    <h2 class="cancel-header">We'd love to know why you're cancelling</h2>

    <textarea
      class="cancel-box"
      name="cancelReason"
      id="cancelReason"
      v-model="userInputReason"
      cols="36"
      rows="10"
      placeholder="Type why you are leaving Bella & Duke"
    ></textarea>

    <p class="cancelling-help-text">
      Can you tell us what food brand you will be moving to?
    </p>
    <!-- :map-keydown="handleBrands" -->
    <v-select
      class="brand-chooser"
      placeholder="Choose food brand"
      :filter="filterBrands"
      :options="dynamicBrands"
      v-model="movingBrand"
      :calculate-position="withPopper"
      taggable
    >
      <span slot="no-options">Type to see options</span></v-select
    >
    <button
      class="bnd-btn white-btn button"
      @click="handleButton({ manageType: 'cancelled' })"
    >
      Cancel Subscription
    </button>
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
import { createPopper } from "@popperjs/core";
export default {
  name: "UserFinalCancel",
  components: {},
  props: {},
  data: () => {
    return {
      movingBrand: "",
      cancelReason: "",
      inputFood: "dog",
      userInputReason: "",
      dynamicBrands: [],
      foodBrands: [
        "Applaws",
        "Arden Grange",
        "Arkwrights",
        "Autarky",
        "AVA",
        "Bakers",
        "Barking Heads",
        "Benyfit Natural",
        "Billy + Margot",
        "Burgess",
        "Burns",
        "Butcher's",
        "Butternut Box",
        "Cesar",
        "Chappie",
        "Chudleys",
        "Cotswold Raw",
        "Crave",
        "Different Dog",
        "Edgard & Cooper",
        "Ella & Co",
        "Eukanuba",
        "Fish4Dogs",
        "Fishmonger's Finest",
        "Forthglade",
        "Gelert Country Choice",
        "Go-Raw",
        "Green Pantry",
        "Harringtons",
        "HiLife",
        "Hills",
        "Iams",
        "Jack Wolf",
        "James Wellbeloved",
        "Laughing Dog",
        "Lily's Kitchen",
        "Natural Instinct",
        "Naturaw",
        "Nature's Harvest",
        "Naturediet",
        "Natures Menu",
        "Naturo",
        "Nutriment",
        "Paleo Ridge",
        "Pedigree",
        "Pooch & Mutt",
        "Poppy's Picnic",
        "Pro Dog Raw",
        "Pro Plan",
        "Pure Pet Food",
        "Purina",
        "RaaW",
        "Raw Made Simple",
        "Rocketo",
        "Royal Canin",
        "Scrumbles",
        "Skinner's",
        "Step Up To Naturals",
        "Tails.com",
        "Taste of the wild",
        "The Easy Raw Dog Food Co.",
        "The Farmers Dog",
        "Truline",
        "Vet's Kitchen",
        "Vitalin",
        "Wafcol",
        "Wagg",
        "Wainright's",
        "Walker & Drake",
        "Winalot",
      ],
    };
  },
  methods: {
    filterBrands(options, search) {
      if (search.length < 2) return [];
      else {
        return this.foodBrands.filter((option) => {
          return option.includes(search);
        });
      }
    },
    // handleBrands: (keyCodes, vm) => ({
    //     ...keyCodes, 50: e => {
    //         console.log(e)
    //         console.log(vm.search)
    //     }
    // }),
    handleButton(manageType) {
      manageType.cancelReason = this.cancelReason;
      manageType.movingBrand = this.movingBrand;
      this.$emit("manageSubmit", manageType);
    },
    withPopper(dropdownList, component, { width }) {
      /**
       * We need to explicitly define the dropdown width since
       * it is usually inherited from the parent with CSS.
       */
      dropdownList.style.width = width;
      /**
       * Here we position the dropdownList relative to the $refs.toggle Element.
       *
       * The 'offset' modifier aligns the dropdown so that the $refs.toggle and
       * the dropdownList overlap by 1 pixel.
       *
       * The 'toggleClass' modifier adds a 'drop-up' class to the Vue Select
       * wrapper so that we can set some styles for when the dropdown is placed
       * above.
       */
      const popper = createPopper(component.$refs.toggle, dropdownList, {
        placement: this.placement,
        modifiers: [
          {
            name: "offset",
            options: {
              offset: [0, -1],
            },
          },
          {
            name: "toggleClass",
            enabled: true,
            phase: "write",
            fn({ state }) {
              component.$el.classList.toggle(
                "drop-up",
                state.placement === "top"
              );
            },
          },
        ],
      });
      /**
       * To prevent memory leaks Popper needs to be destroyed.
       * If you return function, it will be called just before dropdown is removed from DOM.
       */
      return () => popper.destroy();
    },
  },
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
  font-weight: 600;
  margin: 20px 5px 5px;
  padding: 0 20px;
  font-size: 14px;
}

.cancel-img {
  height: 100px;
}

.cancel-link {
  color: #789904;
  text-decoration: underline;
}

.bnd-btn {
  width: 300px;
}
.cancel-box {
  font-family: Montserrat;
  padding: 10px;
  margin: 10px;
}
</style>

<style >
.brand-chooser {
  margin: 20px 0;
}
.vs__dropdown-toggle,
.vs__search::placeholder,
.vs__dropdown-menu {
  width: 289px;
  background: #ffffff;
  color: #00263a;
  font-family: Montserrat;
  /* margin: 20px 0; */
}

.brand-chooser .vs__dropdown-toggle,
.brand-chooser .vs__dropdown-menu .vs__dropdown-toggle,
.vs__dropdown-menu {
  border: #00263a 1px solid !important;
}

.brand-chooser .vs__clear,
.brand-chooser .vs__open-indicator {
  cursor: pointer;
  fill: #00263a;
}

[data-popper-placement="top"] {
  border-radius: 4px 4px 0 0;
  border-top-style: solid;
  border-bottom-style: solid;
  box-shadow: 0 -3px 6px rgba(0, 0, 0, 0.15);
}
</style>
