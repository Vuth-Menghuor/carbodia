<template>
  <div class="card">
    <div class="wrapper">
      <div class="left-section">
        <div class="details">
          <h3 class="model-name">{{ model }}</h3>
          <p class="price">{{ price }}</p>
        </div>

        <button class="reserve-btn" @click="reserveCar(id)">Reserve Now</button>

        <div class="actions">
          <button class="details-btn" @click="goToProduct(id)">
            View Detail
          </button>
          <button class="delete-btn" @click="removeBookmark(id)">
            Remove Card
          </button>
        </div>
      </div>

      <div class="image-container">
        <img class="bm-img" :src="image" :alt="model" />
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from "pinia";
import { useUsersStore } from "../../stores/users";

export default {
  props: {
    model: String,
    price: String,
    id: String,
    image: String,
  },
  methods: {
    goToProduct(id) {
      this.$router.push(`/car/${id}`);
    },
    reserveCar(id) {
      // Handle reserve action - could navigate to checkout or show modal
      this.$router.push(`/checkout/${id}`);
    },
  },
  computed: {
    ...mapState(useUsersStore, {
      bookmarks: "bookmarks",
      removeBookmark: "removeBookmark",
    }),
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Rajdhani:wght@300;400;500;600;700&display=swap");
.card {
  width: 100%;
  max-width: 938px;
  background-color: #ffffff;
  border-radius: 10px;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  border: 1px solid rgba(0, 0, 0, 0.04);
  overflow: hidden;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 16px;
  gap: 24px;
}

.left-section {
  display: flex;
  flex-direction: column;
  gap: 12px;
  flex-grow: 1;
  min-width: 0;
}

.image-container {
  flex-shrink: 0;
}

.bm-img {
  width: 320px;
  height: 200px;
  object-fit: cover;
  border-radius: 8px;
  border: 1px solid rgba(0, 0, 0, 0.08);
  transition: transform 0.3s ease;
}

.details {
  padding: 0;
  min-width: 0;
}

.model-name {
  font-size: 24px;
  font-weight: 700;
  margin: 0 0 8px 0;
  font-family: "Inria Sans", sans-serif;
  color: #1a1a1a;
  line-height: 1.3;
  word-wrap: break-word;
}

.price {
  font-size: 20px;
  font-weight: 600;
  color: red;
  margin: 0;
  font-family: "Inria Sans", sans-serif;
}

.actions {
  display: flex;
  flex-direction: row;
  gap: 12px;
  flex-shrink: 0;
}

.details-btn,
.delete-btn {
  padding: 0;
  font-size: 18px;
  font-weight: 500;
  border: none;
  cursor: pointer;
  font-family: "Rajdhani", sans-serif;
  transition: all 0.2s ease;
  min-width: 90px;
  text-align: center;
  display: flex;
  align-items: center;
}

.details-btn {
  background-color: transparent;
  color: #374151;
  border: none;
  padding: 0 !important;
}

.details-btn:hover {
  background-color: rgba(0, 0, 0, 0.05);
  color: #1f2937;
}

.reserve-btn {
  background: linear-gradient(135deg, #dc2626, #b91c1c);
  color: #ffffff;
  border: none;
  padding: 10px 16px;
  cursor: pointer;
  font-family: "Rajdhani", sans-serif;
  font-size: 16px;
  font-weight: 600;
  transition: all 0.2s ease;
  width: 76%;
  text-align: center;
  margin: 8px 0;
  border-radius: 2px;
}

.reserve-btn:hover {
  background: linear-gradient(135deg, #b91c1c, #991b1b);
}

.delete-btn {
  background-color: transparent;
  color: #1f2937;
  border: none;
}

.delete-btn:hover {
  background-color: rgba(31, 41, 55, 0.1);
  color: #111827;
}

.details-btn:active,
.delete-btn:active {
  opacity: 0.8;
}

/* Responsive design */
@media (max-width: 640px) {
  .wrapper {
    flex-direction: column;
    padding: 20px;
    gap: 20px;
    text-align: center;
  }

  .details {
    padding: 0;
  }

  .actions {
    flex-direction: row;
    width: 100%;
    gap: 12px;
  }

  .image-container {
    width: 100%;
    order: -1;
  }

  .details-btn,
  .delete-btn {
    flex: 1;
    min-width: auto;
  }

  .bm-img {
    width: 100%;
    max-width: 360px;
    height: auto;
    aspect-ratio: 16 / 10;
  }

  .reserve-btn {
    width: 100%;
    margin: 4px 0;
  }
}
</style>
