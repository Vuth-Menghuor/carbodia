<script>
import CarHeader from "@/components/car/CarHeader.vue";
import NavComponent from "@/components/navigation/NavComponent.vue";
import CarDescription from "@/components/car/CarDescription.vue";
import Back from "../components/car/Back.vue";
import ContactDealer from "../components/ContactDealer.vue";
import EngineDetails from "../components/EngineDetails.vue";
import CommentSection from "@/components/comment/CommentSection.vue";
import EngineDetailsUnboxed from "../components/EngineDetailsUnboxed.vue";
import FooterComponent from "../components/FooterComponent.vue";
import Breadcrumb from "../components/car/Breadcrumb.vue";
import { mapState } from "pinia";
import { useCarStore } from "../stores/cars";
import { useUtilStore } from "../stores/utils";
import SuggestedCar from "../components/SuggestedCar.vue";

export default {
  setup() {
    const carStore = useCarStore();

    return {
      carStore,
    };
  },
  components: {
    Back,
    CarHeader,
    NavComponent,
    CarDescription,
    ContactDealer,
    EngineDetailsUnboxed,
    CommentSection,
    FooterComponent,
    Breadcrumb,
    SuggestedCar,
  },
  data() {
    return {};
  },
  computed: {
    ...mapState(useCarStore, {
      cars: "cars",
    }),

    car() {
      let c = this.cars.find((car) => car.id === this.$route.params.carId);
      return c;
    },

    ...mapState(useUtilStore, {
      priceUsd(store) {
        return store.formatUsd(this.car.price);
      },
    }),

    showGallery() {
      let curPath = this.$route.path;
      return curPath.split("/").reverse()[0] === "gallery";
    },
    carByBrand() {
      return this.cars.filter((c) => c.brand === this.car.brand);
    },
  },
};
</script>

<template>
  <NavComponent
    v-show="!showGallery"
    :bgColor="'white'"
    :textColor="'black'"
    :borderColor="'#C0C0C0'"
  />
  <div class="container" v-show="car.brand">
    <div v-if="!showGallery" class="main">
      <Breadcrumb :brand="car.brand" :model="car.model" />
      <CarHeader />
      <div class="line">
        <hr />
      </div>
      <div class="listing-body-wrapper">
        <div class="desc-container">
          <CarDescription :description="car.innerDescription" />
          <div class="line-grey">
            <hr />
          </div>
          <div class="engine-details">
            <EngineDetailsUnboxed />
          </div>
          <div class="line-grey">
            <hr />
          </div>
          <div class="comment-section">
            <CommentSection />
          </div>
        </div>
        <div class="contact-dealer">
          <ContactDealer />
        </div>
      </div>
      <div class="line">
        <hr />
        <h1>You Might Also Like</h1>
      </div>
    </div>
    <div v-else>
      <RouterView />
    </div>
  </div>
  <div class="suggested-car-container">
    <template v-for="car in carByBrand.slice(0, 3)">
      <SuggestedCar :car="car" />
    </template>
  </div>
  <FooterComponent />
</template>

<style scoped>
.line {
  padding: 30px 136px;
}

.line h1 {
  font-family: "Rajdhani", sans-serif;
  font-size: 32px;
  font-weight: 700;
  color: #111827;
  margin: 20px 0 0 0;
}

.line hr {
  border: none;
  border-top: 1px solid #e5e7eb;
  margin: 0;
}

.line-grey {
  margin: 30px 0;
  padding-right: 30px;
}

.line-grey hr {
  border: none;
  border-top: 1px solid #e5e7eb;
}

.listing-body-wrapper {
  display: flex;
  gap: 40px;
  padding: 0 136px;
  background-color: #ffffff;
  box-sizing: border-box;
}

.desc-container {
  flex: 1;
  display: flex;
  flex-direction: column;
  max-width: 800px;
}

.comment-section {
  margin-top: 30px;
  padding-right: 30px;
}

.contact-dealer {
  position: sticky;
  top: 100px;
  height: fit-content;
  width: 350px;
  flex-shrink: 0;
}

.engine-details {
  padding-right: 30px;
}

.suggested-car-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(380px, 1fr));
  gap: 24px;
  padding: 40px 136px;
  background-color: #f9fafb;
  box-sizing: border-box;
}

@media (max-width: 1200px) {
  .line,
  .listing-body-wrapper,
  .suggested-car-container {
    padding-left: 60px;
    padding-right: 60px;
  }
}

@media (max-width: 992px) {
  .listing-body-wrapper {
    flex-direction: column;
  }

  .contact-dealer {
    position: relative;
    top: 0;
    width: 100%;
    max-width: 600px;
    margin: 0 auto;
  }

  .desc-container {
    max-width: 100%;
  }
}

@media (max-width: 768px) {
  .line,
  .listing-body-wrapper,
  .suggested-car-container {
    padding-left: 20px;
    padding-right: 20px;
  }

  .suggested-car-container {
    grid-template-columns: 1fr;
  }

  .line {
    padding-top: 24px;
    padding-bottom: 24px;
  }

  .line h1 {
    font-size: 28px;
  }

  .line-grey,
  .engine-details,
  .comment-section {
    padding-right: 0;
  }
}

@media (max-width: 480px) {
  .line,
  .listing-body-wrapper,
  .suggested-car-container {
    padding-left: 16px;
    padding-right: 16px;
  }

  .listing-body-wrapper {
    gap: 28px;
  }
}
</style>
