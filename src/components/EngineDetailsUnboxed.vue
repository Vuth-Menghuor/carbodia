<template>
  <h2>Car Details</h2>
  <div class="box">
    <div class="info-item">
      <span>
        <calender />
        <span class="space">Year</span>
      </span>
      <span class="space1">{{ engine.year }}</span>
    </div>
    <div class="info-item">
      <span class="name">
        <Key />
        <span class="space">Number of Owners</span>
      </span>
      <span class="space1">{{ engine.ownerNumbers }}</span>
    </div>
    <div class="info-item">
      <span>
        <location />
        <span class="space">Location</span>
      </span>
      <span class="space1">{{ engine.location }}</span>
    </div>
    <div class="info-item">
      <span>
        <Mileage />
        <span class="space">Mileage</span>
      </span>
      <span class="space1">{{ engine.mileage }} km</span>
    </div>
    <div class="info-item">
      <span>
        <Engine />
        <span class="space">Engine</span>
      </span>
      <span class="space1">{{ engine.cylinder }}</span>
    </div>
    <div class="info-item">
      <span>
        <FuleTpye />
        <span class="space">Fuel Type</span>
      </span>
      <span class="space1">{{ engine.fuelType }}</span>
    </div>
    <div class="info-item">
      <span>
        <Power />
        <span class="space">Power</span>
      </span>
      <span class="space1">{{ engine.power }} hp</span>
    </div>
    <div class="info-item">
      <span>
        <color />
        <span class="space">Color</span>
      </span>
      <span class="space1">{{ engine.color }}</span>
    </div>
  </div>
</template>

<script>
import { mapState } from "pinia";
import Calender from "./icons/nameIcon/calender.vue";
import Engine from "./icons/nameIcon/engine.vue";
import FuleTpye from "./icons/nameIcon/fule tpye.vue";
import Key from "./icons/nameIcon/key.vue";
import Location from "./icons/nameIcon/location.vue";
import Mileage from "./icons/nameIcon/mileage.vue";
import Power from "./icons/nameIcon/power.vue";
import { useCarStore } from "../stores/cars";
import color from "./icons/nameIcon/color.vue";

export default {
  name: "CarInfo",
  components: {
    Calender,
    Engine,
    FuleTpye,
    Key,
    Location,
    Mileage,
    Power,
    color,
  },
  data() {
    return {
      carInfo: {
        year: 2021,
        owners: 1,
        location: "Dubai",
        mileage: 0,
        engine: "12 Cylinder",
        fuelType: "Petrol",
        power: 949,
        color: "Cherry",
      },
    };
  },
  computed: {
    ...mapState(useCarStore, {
      car(store) {
        console.log(store.cars[0].brand);
        console.log(this.$route.params.carId);
        return store.getCar(this.$route.params.carId);
      },
    }),
    engine() {
      const engine = this.car.engine;
      if (engine) {
        return engine;
      }
      return {};
    },
  },
};
</script>

<style scoped>
h2 {
  font-family: "Rajdhani", sans-serif;
  font-weight: 700;
  font-size: 28px;
  color: #111827;
  margin: 0 0 24px 0;
}

.box {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 16px;
  background-color: #ffffff;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  padding: 24px;
  font-size: 16px;
  font-weight: 400;
  width: 100%;
  box-sizing: border-box;
}

.info-item {
  display: flex;
  font-family: "Rajdhani", sans-serif;
  justify-content: space-between;
  align-items: center;
  background: #f9fafb;
  border: 1px solid #e5e7eb;
  border-radius: 6px;
  padding: 16px;
}

.info-item span {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 15px;
  color: #374151;
}

.space {
  font-weight: 500;
  color: #6b7280;
}

.space1 {
  font-weight: 600;
  color: #111827;
}

.info-item span svg {
  width: 24px;
  height: 24px;
}

@media (max-width: 480px) {
  h2 {
    font-size: 24px;
    margin-bottom: 16px;
  }

  .box {
    grid-template-columns: 1fr;
    padding: 16px;
    gap: 12px;
  }

  .info-item {
    padding: 12px;
  }

  .info-item span {
    font-size: 14px;
  }
}
</style>
