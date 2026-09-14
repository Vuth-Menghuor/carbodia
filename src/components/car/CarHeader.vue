<template>
  <div class="car-header">
    <div class="image-section">
      <!-- Main Image -->
      <div class="main-image-wrapper">
        <RouterLink
          :to="`/car/${$route.params.carId}/gallery`"
          class="image-link"
        >
          <img :src="imageUrls[0]" alt="Main car image" class="main-image" />
          <div v-if="car.discount" class="discount-badge">
            {{ car.discount }}% OFF
          </div>
        </RouterLink>
      </div>

      <!-- Thumbnail Gallery -->
      <div class="thumbnail-gallery">
        <RouterLink
          v-for="(img, index) in imageUrls.slice(1, 4)"
          :key="index"
          :to="`/car/${$route.params.carId}/gallery`"
          class="thumbnail-link"
        >
          <img
            :src="img"
            :alt="`Car image ${index + 2}`"
            class="thumbnail-image"
          />
        </RouterLink>

        <!-- View All Photos Overlay -->
        <RouterLink
          :to="`/car/${$route.params.carId}/gallery`"
          class="thumbnail-link overlay-link"
        >
          <img
            :src="imageUrls[imageUrls.length - 1]"
            :alt="`Car image ${imageUrls.length}`"
            class="thumbnail-image"
          />
          <div v-if="car.images.length > 5" class="view-all-overlay">
            <span class="view-all-text"
              >View All Photos ({{ car.images.length }})</span
            >
          </div>
        </RouterLink>
      </div>
    </div>

    <div class="price-sec">
      <div class="car-details">
        <h2 class="title">{{ car.model }}</h2>
        <p class="subtitle">{{ car.location }}</p>
      </div>
      <div class="price-inquire">
        <div class="price-wrapper">
          <p v-if="car.discount" class="price">
            <span class="original-price">
              <del>{{ formatUsd(car.price) }}</del>
            </span>
            <span class="discounted-price">{{
              formatUsd(discountedPrice(car.price, car.discount))
            }}</span>
          </p>
          <p v-else class="price">{{ formatUsd(car.price) }}</p>
        </div>
        <RouterLink :to="`/checkout/${car.id}`">
          <button @click="inquire" class="inquire-button">Reserve Now</button>
        </RouterLink>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from "pinia";
import { useCarStore } from "../../stores/cars";
import { useUtilStore } from "../../stores/utils";

export default {
  name: "CarHeader",
  // methods: {
  //   inquire() {
  //     alert("Inquire button clicked!");
  //   },
  // },
  computed: {
    ...mapState(useCarStore, {
      car(store) {
        return store.getCar(this.$route.params.carId);
      },
      imageUrls(store) {
        const urls = [];
        this.car.images.forEach((img) => {
          urls.push(store.getImageURL("cars", this.$route.params.carId, img));
        });
        return urls;
      },
      discountedPrice: "getDiscountedPrice",
    }),

    ...mapState(useUtilStore, {
      formatUsd: "formatUsd",
    }),
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Inria+Sans:ital,wght@0,300;0,400;0,700;1,300;1,400;1,700&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Lora:ital,wght@0,400..700;1,400..700&display=swap");

.car-header {
  padding: 10px 136px 0 136px;
  box-sizing: border-box;
}

/* Image Section - Flexbox Layout */
.image-section {
  display: flex;
  flex-direction: row;
  gap: 12px;
}

/* Main Image */
.main-image-wrapper {
  flex: 1;
  position: relative;
}

.image-link {
  display: block;
  position: relative;
  width: 100%;
  height: 100%;
}

.main-image {
  width: 100%;
  height: 500px;
  object-fit: cover;
  border-radius: 6px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

/* Discount Badge */
.discount-badge {
  position: absolute;
  bottom: 16px;
  right: 0;
  background: linear-gradient(135deg, #ff6f00, #ff8f00);
  color: white;
  padding: 10px 20px;
  font-family: "Rajdhani", sans-serif;
  font-weight: 600;
  font-size: 16px;
  border-radius: 8px 0 0 8px;
  box-shadow: 0 4px 12px rgba(255, 111, 0, 0.4);
}

/* Thumbnail Gallery */
.thumbnail-gallery {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(2, 1fr);
  gap: 12px;
  flex: 1;
}

.thumbnail-link {
  position: relative;
  display: block;
  overflow: hidden;
  border-radius: 6px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.thumbnail-image {
  width: 100%;
  height: 244px;
  object-fit: cover;
}

/* View All Overlay */
.overlay-link {
  position: relative;
}

.view-all-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 6px;
  transition: background 0.3s ease;
}

.overlay-link:hover .view-all-overlay {
  background: rgba(0, 0, 0, 0.7);
}

.view-all-text {
  color: white;
  font-family: "Rajdhani", sans-serif;
  font-size: 18px;
  font-weight: 600;
  text-align: center;
}

/* Responsive Design */
@media (max-width: 1200px) {
  .car-header {
    padding-left: 60px;
    padding-right: 60px;
  }
}

@media (max-width: 992px) {
  .image-section {
    flex-direction: column;
  }

  .thumbnail-gallery {
    width: 100%;
    grid-template-columns: repeat(4, 1fr);
  }

  .thumbnail-image {
    height: 180px;
  }
}

@media (max-width: 768px) {
  .car-header {
    padding: 10px 20px 0 20px;
  }

  .image-section {
    padding: 0;
  }

  .main-image {
    height: 350px;
  }

  .thumbnail-gallery {
    grid-template-columns: repeat(2, 1fr);
  }

  .thumbnail-image {
    height: 160px;
  }
}

/* Price Section */
.price-sec {
  padding: 30px 0px 10px 0px;
  background-color: #ffffff;
}

.car-details {
  margin-bottom: 24px;
}

.title {
  font-family: "Rajdhani", sans-serif;
  font-size: 32px;
  font-weight: 700;
  color: #111827;
  margin: 0 0 8px 0;
}

.subtitle {
  font-family: "Rajdhani", sans-serif;
  font-size: 16px;
  font-weight: 400;
  color: #6b7280;
  margin: 0;
}

.price-inquire {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 20px;
  border-top: 1px solid #e5e7eb;
}

.price-wrapper {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.price {
  font-family: "Rajdhani", sans-serif;
  font-size: 36px;
  font-weight: 700;
  color: #111827;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.original-price {
  font-size: 20px;
  font-weight: 500;
  color: #dc2626;
}

.discounted-price {
  font-size: 36px;
  font-weight: 700;
  color: #111827;
}

.inquire-button {
  font-family: "Rajdhani", sans-serif;
  background-color: #dc2626;
  color: white;
  height: 56px;
  width: 300px;
  border: none;
  font-size: 18px;
  font-weight: 600;
  cursor: pointer;
  border-radius: 4px;
}

@media (max-width: 768px) {
  .price-sec {
    padding: 30px 20px;
  }

  .title {
    font-size: 24px;
  }

  .price {
    font-size: 28px;
  }

  .discounted-price {
    font-size: 28px;
  }

  .original-price {
    font-size: 18px;
  }

  .price-inquire {
    flex-direction: column;
    align-items: flex-start;
    gap: 20px;
  }

  .inquire-button {
    width: 100%;
  }
}

@media (max-width: 480px) {
  .car-header {
    padding: 8px 16px 0;
  }

  .main-image {
    height: 260px;
  }

  .thumbnail-gallery {
    gap: 8px;
  }

  .thumbnail-image {
    height: 110px;
  }

  .price-sec {
    padding: 24px 0 8px;
  }

  .price-inquire {
    gap: 16px;
  }

  .inquire-button {
    height: 50px;
  }
}
</style>
