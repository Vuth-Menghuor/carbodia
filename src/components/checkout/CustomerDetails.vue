<template>
  <div v-if="showCustomer" class="container">
    <div class="checkout-steps">
      <div class="step completed">
        <div class="step-circle">
          <span class="step-number">1</span>
        </div>
        <span class="step-label">Deposit</span>
      </div>
      <div class="step-connector completed"></div>
      <div class="step active">
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
      <img :src="imageUrl" :alt="imageUrl" />
      <div class="car-info-section">
        <h1>{{ car.model }}</h1>
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
        <span class="monthly-payment">
          From {{ formatUsd(mapCarLoan[$route.params.carId]) }}/month
        </span>
      </div>
    </div>
    <div>
      <h3>1. Customer Details</h3>
      <div class="row-select-fill">
        <div class="select-fill-content">
          <span>Salutation*</span>
          <select>
            <option value="">Mr</option>
            <option value="">Mrs</option>
            <option value="">Ms</option>
            <option value="">Dr</option>
          </select>
        </div>
        <div class="select-fill-content">
          <span>First Name*</span>
          <span class="text-error">{{ errors.firstname }}</span>
          <input v-model="firstname" v-bind="firstnameProps" type="text" />
        </div>
      </div>
    </div>
    <div>
      <div class="row-select-fill">
        <div class="select-fill-content">
          <span>Last Name*</span>
          <span class="text-error">{{ errors.lastname }}</span>
          <input v-model="lastname" v-bind="lastnameProps" type="text" />
        </div>
        <div class="select-fill-content">
          <span>Email*</span> <span class="text-error">{{ errors.email }}</span>
          <input v-model="email" v-bind="emailProps" type="email" />
        </div>
      </div>
    </div>
    <div>
      <div class="row-select-fill">
        <div class="select-fill-content">
          <span>Date of Birth*</span>
          <span class="text-error">{{ errors.dob }}</span>
          <input v-model="dob" v-bind="dobProps" type="date" />
        </div>
        <div class="select-fill-content">
          <span>Gender</span>
          <select>
            <option value="">Male</option>
            <option value="">Female</option>
          </select>
        </div>
      </div>
    </div>
    <div>
      <div class="row-select-fill">
        <div class="select-fill-content">
          <span>City*</span> <span class="text-error">{{ errors.city }}</span>
          <input v-model="city" v-bind="cityProps" type="text" />
        </div>
        <div class="select-fill-content">
          <span>Country*</span>
          <select id="country" name="country" class="form-control">
            <option value="Cambodia">Cambodia</option>
            <option value="Zimbabwe">Zimbabwe</option>
          </select>
        </div>
      </div>
    </div>
    <div>
      <div class="row-select-fill">
        <div class="select-fill-content">
          <span>Telephone</span>
          <div class="fill-telephone">
            <div class="phone-icon-wrapper">
              <span class="phone-icon">+</span>
              <input type="text" placeholder="855" />
            </div>
            <input
              type="text"
              class="phone-number"
              placeholder="Phone number"
            />
          </div>
        </div>
        <div class="select-fill-content">
          <span>Address</span>
          <input type="text" />
        </div>
      </div>
    </div>
  </div>
  <div v-else>
    <RouterView />
  </div>
</template>

<script>
import { mapState } from "pinia";
import { useCarStore } from "../../stores/cars";
import { useUtilStore } from "../../stores/utils";
import { useUsersStore } from "../../stores/users";
import { string, date } from "yup";
import { useForm } from "vee-validate";

export default {
  setup() {
    const emailValidator = string().required("Email is required").email();
    const firsnameValidator = string().required("First name is required");
    const lastnameValidator = string().required("Last name is required");
    const dobValidator = date().max(new Date(), "You are lying");
    const cityValidator = string().required("City is required");

    const { defineField, errors } = useForm({
      validationSchema: {
        email: emailValidator,
        firstname: firsnameValidator,
        lastname: lastnameValidator,
        dob: dobValidator,
        city: cityValidator,
      },
    });

    const [email, emailProps] = defineField("email");
    const [firstname, firstnameProps] = defineField("firstname");
    const [lastname, lastnameProps] = defineField("lastname");
    const [dob, dobProps] = defineField("dob");
    const [city, cityProps] = defineField("city");

    return {
      errors,
      firstname,
      firstnameProps,
      lastname,
      lastnameProps,
      email,
      emailProps,
      dob,
      dobProps,
    };
  },
  data() {
    return {
      showCustomer: false,
    };
  },
  computed: {
    showCustomer() {
      let curPath = this.$route.path;
      return this.$route.name === "customer-details";
    },
    ...mapState(useCarStore, {
      cars: "cars",
      imageUrl(store) {
        return store.getImageURL("cars", this.car.id, this.car.images[0]);
      },
    }),
    car() {
      return this.cars.find((c) => c.id === this.$route.params.carId);
    },
    ...mapState(useUtilStore, {
      formatUsd: "formatUsd",
    }),
    ...mapState(useCarStore, {
      cars: "cars",
      imageUrl(store) {
        return store.getImageURL("cars", this.car.id, this.car.images[0]);
      },
      discountedPrice: "getDiscountedPrice",
    }),
    ...mapState(useUsersStore, {
      mapCarLoan: "mapCarLoan",
    }),
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
};
</script>

<style scoped>
.container {
  padding: 10px 136px 100px 136px;
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

.collapse-item {
  padding: 30px;
  margin-bottom: 20px;
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  border: 1px solid #e0e0e0;
}

.collapse-item h3 {
  font-family: "Rajdhani", sans-serif;
  font-size: 24px;
  font-weight: 700;
  color: #333;
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  gap: 10px;
}

.item-row {
  display: flex;
  align-items: start;
  gap: 40px;
  background: #fff;
  border-radius: 12px;
}

@media (max-width: 768px) {
  .item-row {
    flex-direction: column;
    gap: 20px;
    text-align: center;
  }

  .item-row img {
    width: 100%;
    max-width: 300px;
    height: auto;
  }

  .content-row {
    gap: 10px;
  }
}

.image-container {
  flex-shrink: 0;
}

.item-row img {
  height: auto;
  border: 1px solid rgba(0, 0, 0, 0.08);
  border-radius: 12px;
  width: 45%;
  min-width: 300px;
  object-fit: cover;
}

.content-row {
  display: flex;
  flex-direction: column;
  gap: 0;
  flex: 1;
  justify-content: start;
  align-items: start;
  padding: 0;
}

h1 {
  font-size: 32px;
  font-family: "Rajdhani", sans-serif;
  font-weight: 700;
  color: #111;
  margin: 0;
  line-height: 1.2;
  padding-bottom: 2px;
}

.price-label {
  font-size: 16px;
  font-family: "Rajdhani", sans-serif;
  font-weight: 600;
  color: #666;
  margin-bottom: 5px;
  display: block;
}

.price-display h3 {
  font-size: 28px;
  font-family: "Rajdhani", sans-serif;
  font-weight: 800;
  color: #dc2626;
  margin: 0;
  line-height: 1.3;
}

.original-price {
  font-size: 20px;
  color: #999;
  margin-right: 10px;
}

.original-price del {
  text-decoration: line-through;
}

.monthly-payment {
  font-size: 18px;
  color: #555;
  font-weight: 600;
  line-height: 1.3;
  margin-top: 10px;
  display: block;
}

.row-select-fill {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
  padding-top: 20px;
  align-items: end;
}

.select-fill-content {
  display: flex;
  flex-direction: column;
  gap: 10px;
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

.select-fill-content input {
  font-size: 16px;
  outline: none;
  border-radius: 6px;
  border: 1px solid #ccc;
  background-color: white;
  padding: 20px;
  transition: border-color 0.3s ease;
  appearance: none;
  background-repeat: no-repeat;
  background-position: right 15px center;
  background-size: 30px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.select-fill-content select:focus {
  border-color: #000000;
}

.select-fill-content > span {
  font-family: "Rajdhani", sans-serif;
  font-size: 16px;
  color: #333;
}

.select-fill-content > .text-error {
  color: red;
}

.select-fill-content > .border-error {
  border-color: red;
}

.fill-telephone {
  display: flex;
  gap: 10px;
}

.phone-icon-wrapper {
  display: flex;
  align-items: center;
  position: relative;
}

.phone-icon {
  position: absolute;
  left: 16px;
  font-size: 16px;
  color: gray;
}

.phone-icon-wrapper input {
  padding-left: 31px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}

.phone-number {
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 14px;
}

.fill-telephone > .phone-number {
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

.step.completed .step-circle {
  background: linear-gradient(135deg, #6b7280, #4b5563);
  border: 2px solid #6b7280;
}

.step.completed .step-number {
  color: #fff;
}

.step.completed .step-label {
  color: #6b7280;
  font-weight: 600;
}

.step-connector.completed {
  background-color: #6b7280;
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

.image-wrapper > img {
  height: auto;
  border: 1px solid rgba(0, 0, 0, 0.08);
  border-radius: 12px;
  width: 45%;
  min-width: 300px;
  object-fit: cover;
}

.car-info-section {
  flex: 1;
  display: flex;
  flex-direction: column;
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

.regular-price {
  font-family: "Rajdhani", sans-serif;
  font-size: 28px;
  font-weight: 700;
  margin: 0;
  color: #1f2937;
}

.monthly-payment {
  font-family: "Rajdhani", sans-serif;
  font-size: 18px;
  color: #555;
  font-weight: 600;
  line-height: 1.3;
  margin-top: 10px;
  display: block;
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
</style>
