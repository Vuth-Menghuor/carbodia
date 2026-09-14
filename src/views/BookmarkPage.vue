<script>
import { mapState } from "pinia";
import { useUsersStore } from "@/stores/users";
import { useUtilStore } from "@/stores/utils";
import SimpleCarCard from "@/components/car/SimpleCarCard.vue";
import NavComponent from "@/components/navigation/NavComponent.vue";
import { useCarStore } from "../stores/cars";

export default {
  setup() {
    const userStore = useUsersStore();
    const utilStore = useUtilStore();
    console.log(userStore.bookmarks.length);
    return {
      userStore,
      utilStore,
    };
  },
  components: {
    SimpleCarCard,
    NavComponent,
  },
  computed: {
    ...mapState(useUsersStore, {
      bookmarks: "bookmarks",
    }),
    ...mapState(useCarStore, {
      imageUrl(store) {
        return (id, img) => store.getImageURL("cars", id, img);
      },
    }),
    ...mapState(useUtilStore, {
      formatUsd: "formatUsd",
    }),
  },
};
</script>

<template>
  <NavComponent text-color="black" />
  <div class="bookmark-page">
    <div class="bookmark-container">
      <header class="bookmark-header">
        <h1 class="bookmark-title">My Bookmarks</h1>
        <div class="bookmark-count">
          <span class="count-number">{{ bookmarks.length }}</span>
          <span class="count-label">
            {{ bookmarks.length === 1 ? "Vehicle" : "Vehicles" }} Saved
          </span>
        </div>
      </header>

      <div v-if="bookmarks.length === 0" class="empty-state">
        <div class="empty-icon">🔖</div>
        <h3 class="empty-title">No bookmarks yet</h3>
        <p class="empty-description">
          Start browsing and save your favorite vehicles to see them here.
        </p>
      </div>

      <div v-else class="bookmarks-grid">
        <template v-for="car in bookmarks" :key="car.id">
          <SimpleCarCard
            :id="car.id"
            :model="car.model"
            :price="formatUsd(car.price)"
            :image="imageUrl(car.id, car.images[0])"
            class="bookmark-card"
          />
        </template>
      </div>
    </div>
  </div>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap");

.bookmark-page {
  font-family: "Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    sans-serif;
  background-color: #fafafa;
  padding-top: 150px;
  min-height: 100dvh;
  box-sizing: border-box;
}

.bookmark-container {
  max-width: 940px;
  margin: 0 auto;
  padding: 0 24px;
}

.bookmark-header {
  margin-bottom: 40px;
  padding-bottom: 24px;
  border-bottom: 1px solid #e5e7eb;
}

.bookmark-title {
  font-size: 30px;
  font-weight: 700;
  color: #111827;
  margin: 0 0 12px 0;
  line-height: 1.2;
}

.bookmark-count {
  display: flex;
  align-items: baseline;
  gap: 8px;
}

.count-number {
  font-size: 1.125rem;
  font-weight: 600;
  color: #3b82f6;
  background: #eff6ff;
  padding: 4px 12px;
  border-radius: 20px;
  border: 1px solid #dbeafe;
}

.count-label {
  font-size: 0.875rem;
  color: #6b7280;
  font-weight: 500;
}

.empty-state {
  text-align: center;
  padding: 80px 20px;
  background: white;
  border-radius: 16px;
  border: 1px solid #e5e7eb;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1);
}

.empty-icon {
  font-size: 4rem;
  margin-bottom: 24px;
  opacity: 0.6;
}

.empty-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: #374151;
  margin: 0 0 12px 0;
}

.empty-description {
  font-size: 1rem;
  color: #6b7280;
  margin: 0;
  max-width: 400px;
  margin: 0 auto;
  line-height: 1.5;
}

.bookmarks-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 24px;
  margin-bottom: 40px;
}

.bookmark-card {
  transition: all 0.2s ease;
  border-radius: 12px;
  overflow: hidden;
  background: white;
  border: 1px solid #e5e7eb;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1);
}

/* Responsive Design */
@media (max-width: 768px) {
  .bookmark-page {
    padding-top: 128px;
  }

  .bookmark-container {
    padding: 0 16px;
  }

  .bookmark-title {
    font-size: 2rem;
  }

  .bookmarks-grid {
    grid-template-columns: 1fr;
    gap: 16px;
  }

  .bookmark-header {
    margin-bottom: 24px;
    padding-bottom: 20px;
  }

  .empty-state {
    padding: 60px 20px;
  }
}

@media (max-width: 480px) {
  .bookmark-container {
    padding: 0 12px;
  }

  .bookmark-title {
    font-size: 1.75rem;
  }

  .bookmark-count {
    flex-direction: column;
    align-items: flex-start;
    gap: 4px;
  }

  .empty-state {
    padding: 44px 16px;
    border-radius: 12px;
  }

  .empty-icon {
    font-size: 3rem;
    margin-bottom: 16px;
  }
}

/* Focus states for accessibility */
.bookmark-card:focus-within {
  outline: 2px solid #3b82f6;
  outline-offset: 2px;
}
</style>
