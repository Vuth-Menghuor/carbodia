<template>
  <div class="container">
    <div class="checkout-steps">
      <div class="step completed">
        <div class="step-circle">
          <span class="step-number">1</span>
        </div>
        <span class="step-label">Deposit</span>
      </div>
      <div class="step-connector completed"></div>
      <div class="step completed">
        <div class="step-circle">
          <span class="step-number">2</span>
        </div>
        <span class="step-label">Customer Details</span>
      </div>
      <div class="step-connector completed"></div>
      <div class="step active">
        <div class="step-circle">
          <span class="step-number">3</span>
        </div>
        <span class="step-label">Payment</span>
      </div>
    </div>
    <h3>Selected Vehicle</h3>
    <div class="image-wrapper">
      <img :src="imageUrl" :alt="imageUrl" />
      <div class="car-info-section">
        <h1>{{ car.model }}</h1>
        <div class="car-details">
          <span class="car-location">{{
            car.location || "Porsche Centre Phnom Penh City, Cambodia"
          }}</span>
          <span class="car-telephone">Telephone: +(855) 999 777 888</span>
        </div>
      </div>
    </div>
    <div class="payment-terms">
      <label>Please accept Payments to proceed</label>
      <div class="payment-consent">
        <label>Payment Consent*</label>
        <div class="payment-checkbox">
          <div class="checkbox-wrapper-30">
            <span class="checkbox">
              <input v-model="termAgreed" type="checkbox" />
              <svg>
                <use xlink:href="#checkbox-30" class="checkbox"></use>
              </svg>
            </span>
            <svg xmlns="http://www.w3.org/2000/svg" style="display: none">
              <symbol id="checkbox-30" viewBox="0 0 22 22">
                <path
                  fill="none"
                  stroke="currentColor"
                  d="M5.5,11.3L9,14.8L20.2,3.3l0,0c-0.5-1-1.5-1.8-2.7-1.8h-13c-1.7,0-3,1.3-3,3v13c0,1.7,1.3,3,3,3h13 c1.7,0,3-1.3,3-3v-13c0-0.4-0.1-0.8-0.3-1.2"
                />
              </symbol>
            </svg>
          </div>
          <span>I agree to the Vehicle Reservation Terms & Conditions.</span>
        </div>
      </div>
      <div class="confirm-section">
        <span>Reservation Deposit</span>
        <button @click="handleSubmit()">Confirm</button>
      </div>
    </div>
    <div v-show="openModal">
      <SuccessModal />
    </div>
  </div>
</template>
<script>
import CheckCompleted from "../icons/payment/checkCompleted.vue";
import { useUsersStore } from "../../stores/users";
import { mapState } from "pinia";
import { useCarStore } from "../../stores/cars";
import SuccessModal from "../SuccessModal.vue";

export default {
  components: {
    CheckCompleted,
    SuccessModal,
  },
  data() {
    return {
      termAgreed: false,
      openModal: false,
    };
  },
  async mounted() {
    await this.$router.isReady();
    const usersStore = useUsersStore();
    let id = this.$route.params.carId;
    if (!usersStore.mapCarLoan[id]) {
      this.$router.push({
        name: "checkout",
        params: {
          carId: id,
        },
      });
    }
  },
  methods: {
    handleSubmit() {
      if (!this.termAgreed) {
        this.openModal = false;
      } else {
        this.openModal = true;
      }
    },
  },
  computed: {
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
  },
};
</script>

<style scoped>
.container {
  padding: 10px 136px 100px 136px;
  position: relative;
}

.row-scroll-wrapper {
  display: flex;
  align-items: center;
  gap: 40px;
}

.customer-completed {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 20px 0px 20px 0px;
}

.customer-completed label {
  color: black;
  font-size: 18px;
  font-family: "Rajdhani", sans-serif;
  font-weight: 500;
}

.payment-completed {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 20px 0px 20px 0px;
}

.payment-completed span {
  background-color: transparent;
  color: black;
  border: 1px solid black;
  padding: 4px 9px;
  font-size: 16px;
  font-weight: 500;
  border-radius: 100%;
}

.payment-completed label {
  font-size: 18px;
  font-family: "Rajdhani", sans-serif;
  font-weight: 500;
  color: black;
}

img {
  height: auto;
  width: 45%;
  border: 1px solid rgba(0, 0, 0, 0.08);
  border-radius: 12px;
  min-width: 300px;
  object-fit: cover;
}

h3 {
  font-weight: 600;
  font-family: "Rajdhani", sans-serif;
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

.car-info-section {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

h1 {
  font-family: "Rajdhani", sans-serif;
  font-size: 32px;
  font-weight: 700;
  color: #1f2937;
  margin: 0;
  line-height: 1.2;
}

.car-details {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.car-location {
  font-family: "Rajdhani", sans-serif;
  font-size: 15px;
  color: #6b7280;
  font-weight: 400;
}

.car-telephone {
  font-family: "Rajdhani", sans-serif;
  font-size: 15px;
  color: #6b7280;
  font-weight: 400;
}

.payment-terms {
  padding-top: 40px;
}

.payment-terms label {
  font-family: "Rajdhani", sans-serif;
  font-weight: 600;
  font-size: 22px;
}

.payment-consent {
  border-radius: 10px;
  margin-top: 30px;
  padding: 30px;
  border: 1px solid gray;
}

.payment-consent label {
  font-size: 18px;
  color: black;
}

.payment-checkbox {
  display: flex;
  align-items: center;
  gap: 10px;
  padding-top: 30px;
}

.payment-checkbox span {
  font-family: "Rajdhani", sans-serif;
}

.confirm-section {
  display: flex;
  flex-direction: column;
  padding-top: 20px;
  gap: 10px;
}

.confirm-section button {
  padding: 20px;
  font-family: "Rajdhani", sans-serif;
  background-color: white;
  border: 1px solid black;
  border-radius: 8px;
  font-size: 18px;
  transition: 0.3s;
  cursor: pointer;
}

.confirm-section button:hover {
  background-color: #ccc;
  cursor: pointer;
  border: 1px solid gray;
}

.confirm-section span {
  display: flex;
  justify-content: center;
  padding: 20px;
  font-family: "Rajdhani", sans-serif;
  background-color: #2d5ea8;
  border: 1px solid #2d5ea8;
  color: white;
  border-radius: 8px;
  font-size: 18px;
}

.checkbox-wrapper-30 .checkbox {
  --bg: #fff;
  --brdr: #d1d6ee;
  --brdr-actv: #1e2235;
  --brdr-hovr: #bbc1e1;
  --dur: calc((var(--size, 2) / 2) * 0.6s);
  display: inline-block;
  width: calc(var(--size, 1) * 22px);
  position: relative;
}

.checkbox-wrapper-30 .checkbox:after {
  content: "";
  width: 100%;
  padding-top: 100%;
  display: block;
}

.checkbox-wrapper-30 .checkbox > * {
  position: absolute;
}

.checkbox-wrapper-30 .checkbox input {
  -webkit-appearance: none;
  -moz-appearance: none;
  -webkit-tap-highlight-color: transparent;
  cursor: pointer;
  background-color: var(--bg);
  border-radius: calc(var(--size, 1) * 4px);
  border: calc(var(--newBrdr, var(--size, 1)) * 1px) solid;
  color: var(--newBrdrClr, var(--brdr));
  outline: none;
  margin: 0;
  padding: 0;
  transition: all calc(var(--dur) / 3) linear;
}

.checkbox-wrapper-30 .checkbox input:hover,
.checkbox-wrapper-30 .checkbox input:checked {
  --newBrdr: calc(var(--size, 1) * 2);
}

.checkbox-wrapper-30 .checkbox input:hover {
  --newBrdrClr: var(--brdr-hovr);
}

.checkbox-wrapper-30 .checkbox input:checked {
  --newBrdrClr: var(--brdr-actv);
  transition-delay: calc(var(--dur) / 1.3);
}

.checkbox-wrapper-30 .checkbox input:checked + svg {
  --dashArray: 16 93;
  --dashOffset: 109;
}

.checkbox-wrapper-30 .checkbox svg {
  fill: none;
  left: 0;
  pointer-events: none;
  stroke: var(--stroke, var(--border-active));
  stroke-dasharray: var(--dashArray, 93);
  stroke-dashoffset: var(--dashOffset, 94);
  stroke-linecap: round;
  stroke-linejoin: round;
  stroke-width: 2px;
  top: 0;
  transition:
    stroke-dasharray var(--dur),
    stroke-dashoffset var(--dur);
}

.checkbox-wrapper-30 .checkbox svg,
.checkbox-wrapper-30 .checkbox input {
  display: block;
  height: 100%;
  width: 100%;
}

.checkout-steps {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  margin-bottom: 30px;
  width: 100%;
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

.step.completed .step-circle {
  background: linear-gradient(135deg, #6b7280, #4b5563);
  border: 2px solid #6b7280;
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

.step.active .step-number,
.step.completed .step-number {
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

.step.completed .step-label {
  color: #6b7280;
  font-weight: 600;
}

.step-connector {
  width: 100px;
  height: 2px;
  background-color: #e0e0e0;
  flex-shrink: 0;
}

.step-connector.completed {
  background-color: #6b7280;
}
</style>
