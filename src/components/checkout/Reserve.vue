<template>
  <div class="back-btn">
    <Back />
  </div>
  <div v-if="showReserve" class="wrapper-content">
    <div class="checkout-steps">
      <div class="step active">
        <div class="step-circle">
          <span class="step-number">1</span>
        </div>
        <span class="step-label">Deposit</span>
      </div>
      <div class="step-connector"></div>
      <div class="step">
        <div class="step-circle">
          <span class="step-number">2</span>
        </div>
        <span class="step-label">Customer Details</span>
      </div>
      <div class="step-connector"></div>
      <div class="step">
        <div class="step-circle">
          <span class="step-number">3</span>
        </div>
        <span class="step-label">Payment</span>
      </div>
    </div>
    <div class="image-wrapper">
      <!-- <img
        src="/Ecommerce/src/assets/images/products/Ferrari-Laferrari/car1.png"
        alt="Ferrari LaFerrari 2017"
      /> -->
      <img :src="imageUrl" :alt="imageUrl" />
      <div class="car-info-section">
        <h1>{{ car.model }}</h1>
        <div class="car-details">
          <span class="car-status">{{ car.status }}</span>
          <span class="car-location">{{ car.location }}</span>
        </div>
        <div class="price-section">
          <span class="price-label">Price</span>
          <div class="price-display">
            <h3 v-if="car.discount" class="discounted-price">
              <span class="original-price">
                <del>{{ formatUsd(car.price) }}</del>
              </span>
              {{ formatUsd(discountedPrice(car.price, car.discount)) }}
            </h3>
            <h3 v-else class="regular-price">{{ formatUsd(car.price) }}</h3>
          </div>
        </div>
      </div>
    </div>
    <div class="container-fill-content">
      <div class="row-select-fill">
        <div class="select-fill-content">
          <span>Finance Product*</span>
          <select>
            <option value="">{{ car.model }}</option>
          </select>
        </div>
        <div class="select-fill-content">
          <span>Tenure*</span>
          <select v-model="tenure">
            <option value="48">48 Months</option>
            <option value="60">60 Months</option>
          </select>
        </div>
      </div>
      <div class="select-fill-content">
        <span>Interest Rate*</span>
        <select>
          <option value="">{{ interestRate }} p.a.flat</option>
        </select>
      </div>
      <div class="row-select-fill">
        <div class="select-fill-reserve" :class="{ focus: downPayment === 30 }">
          <span>Down Payment*</span>
          <button @click="downPayment = 30">
            {{ formatUsd(discountedPrice(car.price, car.discount || 0) * 0.3) }}
            (30%)
          </button>
        </div>
        <div class="select-fill-reserve" :class="{ focus: downPayment === 50 }">
          <button @click="downPayment = 50">
            {{ formatUsd(discountedPrice(car.price, car.discount || 0) * 0.5) }}
            (50%)
          </button>
        </div>
      </div>
      <div class="row-select-fill">
        <div class="select-fill-reserve" :class="{ focus: downPayment === 30 }">
          <span>Loan Payment*</span>
          <button @click="downPayment = 30">
            {{ formatUsd(discountedPrice(car.price, car.discount || 0) * 0.7) }}
            (70%)
          </button>
        </div>
        <div class="select-fill-reserve" :class="{ focus: downPayment === 50 }">
          <button @click="downPayment = 50">
            {{ formatUsd(discountedPrice(car.price, car.discount || 0) * 0.5) }}
            (50%)
          </button>
        </div>
      </div>
      <div class="btn-payment">
        <button class="btn-payment">
          <span>Month Payment</span>
          <span>{{ formatUsd(monthlyPayment) }}</span>
        </button>
      </div>
    </div>
  </div>
  <div v-else>
    <RouterView />
  </div>
  <RouterLink v-show="showBtnNext" :to="next">
    <div class="btn-next">
      <button :disabled="disableNext">Next</button>
    </div>
  </RouterLink>
</template>

<script>
import { mapState } from "pinia";
import Back from "../car/Back.vue";
import ChevronBack from "../icons/productPage/chevronBack.vue";
import { useCarStore } from "../../stores/cars";
import { useUtilStore } from "../../stores/utils";
import { object } from "yup";
import { useUsersStore } from "../../stores/users";
import { useAuthStore } from "../../stores/auth";

export default {
  components: {
    Back,
    ChevronBack,
  },
  data() {
    return {
      showReserve: false,
      interestRate: 2.99,

      tenure: 48,
      downPayment: 30,
      // loan: 70,
    };
  },
  computed: {
    showReserve() {
      console.log(this.$route.name);
      return this.$route.name === "checkout";
    },
    next() {
      const endpoint = this.$route.name;
      console.log(endpoint);
      if (endpoint === "customer-details") {
        return { name: "payment" };
      } else if (endpoint === "checkout") {
        return { name: "customer-details" };
      }
    },
    showBtnNext() {
      return this.$route.name !== "payment";
    },
    ...mapState(useCarStore, {
      cars: "cars",
      imageUrl(store) {
        return store.getImageURL("cars", this.car.id, this.car.images[0]);
      },
      discountedPrice: "getDiscountedPrice",
    }),
    car() {
      return this.cars.find((c) => c.id === this.$route.params.carId);
    },
    ...mapState(useUtilStore, {
      formatUsd: "formatUsd",
    }),
    ...mapState(useUsersStore, {
      mapCarLoan: "mapCarLoan",
    }),

    ...mapState(useAuthStore, {
      disableNext(store) {
        return store.disableCheckoutNext;
      },
    }),
    monthlyPayment() {
      let loan =
        (this.discountedPrice(this.car.price, this.car.discount || 0) *
          (100 - this.downPayment)) /
        100;
      let result = loan / this.tenure + (loan * this.interestRate) / 100 / 12;
      this.mapCarLoan[this.$route.params.carId] = result;
      return result;
    },
  },
};
</script>

<style scoped>
.back-btn {
  padding-bottom: 80px;
}

.wrapper-content {
  padding: 10px 136px 0 136px;
}

.image-wrapper {
  display: flex;
  justify-content: flex-start;
  align-items: flex-start;
  gap: 40px;
  padding-bottom: 40px;
  padding-top: 10px;
  margin: 0 auto;
  margin-top: 18.72px;
}

h1 {
  font-family: "Rajdhani", sans-serif;
  font-size: 32px;
  font-weight: 700;
  color: #1f2937;
  margin: 0 0 16px 0;
  line-height: 1.2;
}

.image-wrapper > img {
  height: auto;
  border: 1px solid rgba(0, 0, 0, 0.08);
  border-radius: 12px;
  width: 45%;
  min-width: 300px;
  object-fit: cover;
}

.container-fill-content {
  display: flex;
  justify-content: center;
  flex-direction: column;
  margin-bottom: 100px;
}

.span-content {
  display: flex;
  flex-direction: column;
  gap: 12px;
  font-size: 15px;
  padding: 20px 0px 30px 0px;
  color: #555;
  font-family: "Rajdhani", sans-serif;
}

.price-name-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  column-gap: 100px;
  word-spacing: 10px;
}

.price-name-content > span {
  font-size: 16px;
  color: #333;
  font-family: "Rajdhani", sans-serif;
}

.price-name-content h3 {
  font-size: 24px;
  font-weight: 600;
  margin: 0;
  color: #333;
  font-family: "Rajdhani", sans-serif;
}

.car-info-section {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.car-details {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.car-status {
  font-family: "Rajdhani", sans-serif;
  font-size: 16px;
  font-weight: 600;
  color: #059669;
  background: #ecfdf5;
  padding: 6px 12px;
  border-radius: 6px;
  display: inline-block;
  width: fit-content;
}

.car-location {
  font-family: "Rajdhani", sans-serif;
  font-size: 15px;
  color: #6b7280;
  font-weight: 400;
}

.price-section {
  display: flex;
  flex-direction: column;
  gap: 12px;
  padding: 24px 0;
  border-top: 1px solid #e5e7eb;
  border-bottom: 1px solid #e5e7eb;
  margin-top: 8px;
}

.price-label {
  font-family: "Rajdhani", sans-serif;
  font-size: 16px;
  font-weight: 600;
  color: #374151;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.price-display h3 {
  font-family: "Rajdhani", sans-serif;
  font-size: 28px;
  font-weight: 700;
  margin: 0;
  color: #1f2937;
  display: flex;
  align-items: center;
  gap: 12px;
}

.original-price {
  font-size: 18px;
  font-weight: 500;
  color: #dc2626;
}

.original-price del {
  color: #dc2626;
}

.row-select-fill {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
  align-items: end;
  padding-bottom: 20px;
}

.select-fill-content {
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding-bottom: 20px;
}

.select-fill-content select {
  font-size: 16px;
  outline: none;
  border-radius: 6px;
  border: 1px solid #ccc;
  background-color: white;
  padding: 20px;
  transition: border-color 0.3s ease;
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='%23222222'%3E%3Cpath d='M7 10l5 5 5-5H7z'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 15px center;
  background-size: 30px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.select-fill-content select:focus {
  border-color: #000000;
}

.select-fill-content > span {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 16px;
  color: #333;
}

.select-fill-reserve {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.select-fill-reserve button {
  font-size: 16px;
  outline: none;
  border-radius: 6px;
  border: 1px solid #ccc;
  background-color: white;
  padding: 20px;
  transition: border-color 0.3s ease;
  background-position: right 15px center;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  color: gray;
  transition-duration: 0.3s;
}

.select-fill-reserve.focus button {
  border-color: #000000;
  color: black;
  font-weight: bolder;
}

.select-fill-reserve > span {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 16px;
  color: #000000;
}

.btn-payment button {
  display: flex;
  justify-content: space-between;
  padding: 20px 20px 20px 20px;
  font-size: 18px;
  width: 100%;
  border-radius: 6px;
  background-color: #dcdcdc;
  border: none;
  cursor: pointer;
}

.btn-payment span {
  font-weight: 600;
}

.btn-next {
  position: fixed;
  display: flex;
  /* top: 115%; */
  /* margin-top: 30px; */
  bottom: 0;
  justify-content: end;
  background-color: white;
  box-shadow: rgba(0, 0, 0, 0.25) 0px 0.0625em 0.0625em,
    rgba(0, 0, 0, 0.25) 0px 0.125em 0.5em,
    rgba(255, 255, 255, 0.1) 0px 0px 0px 1px inset;
  padding: 10px 0px 10px 0px;
  width: 100%;
}

.btn-next button {
  padding: 16px 40px 16px 40px;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: 600;
  font-size: 14px;
  margin-right: 7%;
  background-color: transparent;
  border: none;
  color: white;
  cursor: pointer;
  background-color: black;
  transition: 0.3s ease;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
}

.original-price {
  font-size: 20px;
  color: red;
}

/* Responsive Design */
@media (max-width: 1024px) {
  .image-wrapper {
    gap: 30px;
    padding-bottom: 30px;
  }

  .image-wrapper > img {
    width: 50%;
    min-width: 250px;
  }

  h1 {
    font-size: 28px;
  }

  .price-display h3 {
    font-size: 24px;
  }
}

@media (max-width: 768px) {
  .image-wrapper {
    flex-direction: column;
    gap: 24px;
    padding: 0 20px 30px 20px;
    align-items: center;
  }

  .image-wrapper > img {
    width: 100%;
    max-width: 400px;
    min-width: unset;
  }

  .car-info-section {
    align-items: center;
    text-align: center;
    gap: 16px;
  }

  h1 {
    font-size: 24px;
    margin-bottom: 12px;
  }

  .car-details {
    gap: 6px;
  }

  .price-section {
    padding: 20px 0;
    gap: 8px;
  }

  .price-display h3 {
    font-size: 22px;
    justify-content: center;
  }

  .original-price {
    font-size: 16px;
  }
}

@media (max-width: 480px) {
  .image-wrapper {
    padding: 0 15px 20px 15px;
  }

  h1 {
    font-size: 20px;
  }

  .price-display h3 {
    font-size: 20px;
    flex-direction: column;
    gap: 8px;
  }

  .car-status {
    font-size: 14px;
    padding: 4px 8px;
  }

  .car-location {
    font-size: 14px;
  }
}

.checkout-steps {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  margin-bottom: 30px;
}

.step {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
}

.step-circle {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
}

.step.active .step-circle {
  background: linear-gradient(135deg, #dc2626, #b91c1c);
  border: 2px solid #dc2626;
}

.step .step-circle {
  background-color: transparent;
  border: 2px solid #ccc;
}

.step-number {
  font-size: 16px;
  font-weight: 600;
  color: inherit;
}

.step.active .step-number {
  color: #fff;
}

.step .step-number {
  color: #666;
}

.step-label {
  font-size: 14px;
  font-weight: 500;
  color: #333;
  text-align: center;
  white-space: nowrap;
}

.step.active .step-label {
  color: #000;
  font-weight: 600;
}

.step-connector {
  width: 100px;
  height: 2px;
  background-color: #e0e0e0;
  flex-shrink: 0;
}
</style>
