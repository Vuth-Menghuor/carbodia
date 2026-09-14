<template>
  <div
    class="related-rides"
    @click="$router.push({ name: 'car', params: { carId: car.id } })"
  >
    <div class="suggested-card">
      <div class="ride-details">
        <div class="img-container">
          <div v-if="car.discount" class="discount-tag">
            {{ car.discount }} % OFF
          </div>
          <img :src="imageUrl" class="ride-image" />
        </div>
        <div class="product-card">
          <div v-if="car.discount">
            <p class="price">
              <span class="original-price">
                <del>
                  {{ formatUsd(car.price) }}
                </del>
              </span>
              {{ formatUsd(discountedPrice) }}
            </p>
          </div>
          <p v-else class="price discounted-price">
            {{ formatUsd(car.price) }}
          </p>
          <h3>{{ car.model }}</h3>
          <span>{{ car.location }}</span>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { mapState } from "pinia";
import { useCarStore } from "../stores/cars";
import { object } from "yup";
import { useUtilStore } from "../stores/utils";

export default {
  props: {
    car: Object,
  },
  computed: {
    ...mapState(useUtilStore, { formatUsd: "formatUsd" }),
    ...mapState(useCarStore, {
      imageUrl(store) {
        return store.getImageURL("cars", this.car.id, this.car.images[0]);
      },
      discountedPrice(store) {
        return store.getDiscountedPrice(this.car.price, this.car.discount);
      },
    }),
  },
};
</script>
<style scoped>
.related-rides {
  text-align: center;
  font-family: "Rajdhani", sans-serif;
  margin: 10px;
  cursor: pointer;
}

.suggested-card {
  display: flex;
  align-items: center;
  margin: 0 auto;
  border: 1px solid #e5e7eb;
  background-color: #ffffff;
  border-radius: 8px;
  overflow: hidden;
}

.ride-details {
  display: flex;
  flex-direction: column;
  width: 100%;
  text-align: left;
}

.img-container {
  position: relative;
  width: 100%;
  height: 300px;
  overflow: hidden;
}

.ride-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.discount-tag {
  position: absolute;
  bottom: 12px;
  right: 0;
  padding: 8px 16px;
  color: white;
  background-color: #dc2626;
  font-weight: 600;
  font-size: 14px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 4px 0 0 4px;
}

.product-card {
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.price {
  font-size: 20px;
  color: #111827;
  font-weight: 700;
  margin: 0;
}

.original-price {
  font-size: 16px;
  color: #dc2626;
  margin-right: 8px;
}

h3 {
  font-weight: 600;
  font-size: 18px;
  color: #111827;
  margin: 0;
}

span {
  font-size: 14px;
  color: #6b7280;
}

@media (max-width: 480px) {
  .related-rides {
    margin: 0;
  }

  .img-container {
    height: 220px;
  }

  .product-card {
    padding: 16px;
  }
}
</style>
