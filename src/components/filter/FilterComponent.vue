<template>
  <div class="filter-panel">
    <button
      class="filter-toggle"
      type="button"
      :aria-expanded="isExpanded"
      @click="isExpanded = !isExpanded"
    >
      <span>Filter cars</span>
      <span class="filter-toggle-icon" :class="{ expanded: isExpanded }">⌄</span>
    </button>

    <div class="filter-content" :class="{ expanded: isExpanded }">
      <!-- Price Section -->
      <div class="filter-section">
      <h3 class="section-title">Price Range</h3>
      <div class="options-container">
        <div
          v-for="option in priceOptions"
          :key="option.value"
          class="option-item"
        >
          <input
            type="radio"
            :id="`price-${option.value}`"
            v-model="selectedPrice"
            :value="option.value"
            name="price"
            class="radio-input"
          />
          <label :for="`price-${option.value}`" class="option-label">
            {{ option.label }}
          </label>
        </div>
      </div>
      </div>

      <!-- Brand Section -->
      <div class="filter-section">
      <h3 class="section-title">Brand</h3>
      <div class="options-container">
        <div
          v-for="brand in brandOptions"
          :key="brand.value"
          class="option-item"
        >
          <input
            type="radio"
            :id="`brand-${brand.value}`"
            v-model="selectedBrand"
            :value="brand.value"
            name="brand"
            class="radio-input"
          />
          <label :for="`brand-${brand.value}`" class="option-label">
            {{ brand.label }}
          </label>
        </div>
      </div>
      </div>

      <!-- Discount Section -->
      <div class="filter-section">
      <h3 class="section-title">Discount</h3>
      <div class="options-container">
        <div
          v-for="discount in discountOptions"
          :key="discount.value"
          class="option-item"
        >
          <input
            type="radio"
            :id="`discount-${discount.value}`"
            v-model="selectedDiscount"
            :value="discount.value"
            name="discount"
            class="radio-input"
          />
          <label :for="`discount-${discount.value}`" class="option-label">
            {{ discount.label }}
          </label>
        </div>
      </div>
      </div>

      <!-- Clear Filters Button -->
      <button @click="clearAllFilters" class="clear-button">
        Clear All Filters
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, watch, onMounted } from "vue";
import { useRoute } from "vue-router";

const route = useRoute();

const selectedPrice = ref(false);
const selectedBrand = ref(false);
const selectedDiscount = ref(false);
const isExpanded = ref(false);

// Define filter options
const priceOptions = [
  { value: false, label: "All Prices" },
  { value: 1000001, label: "Above $1M" },
  { value: 1000000, label: "Under $1M" },
  { value: 500000, label: "Under $500K" },
  { value: 200000, label: "Under $200K" },
  { value: 100000, label: "Under $100K" },
];

const brandOptions = [
  { value: false, label: "All Brands" },
  { value: "ferrari", label: "Ferrari" },
  { value: "mercedes", label: "Mercedes" },
  { value: "porsche", label: "Porsche" },
  { value: "lamborghini", label: "Lamborghini" },
  { value: "bmw", label: "BMW" },
];

const discountOptions = [
  { value: false, label: "All Items" },
  { value: true, label: "Discounted Only" },
];

const emit = defineEmits(["filter-price", "filter-brand", "filter-discount"]);

// Initialize filters
onMounted(() => {
  // Set initial brand from route
  if (route.params.brandName) {
    selectedBrand.value = route.params.brandName;
  }

  // Emit initial values
  emit("filter-price", selectedPrice.value);
  emit("filter-brand", selectedBrand.value);
  emit("filter-discount", selectedDiscount.value);
});

// Watch for changes and emit events
watch(selectedPrice, (newValue) => {
  emit("filter-price", newValue);
});

watch(selectedBrand, (newValue) => {
  emit("filter-brand", newValue);
});

watch(selectedDiscount, (newValue) => {
  emit("filter-discount", newValue);
});

// Clear all filters
function clearAllFilters() {
  selectedPrice.value = false;
  selectedBrand.value = false;
  selectedDiscount.value = false;
}
</script>

<style scoped>
.filter-panel {
  position: relative;
  background: #ffffff;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  padding: 24px;
  max-width: 320px;
  right: 20px;
  top: 16px;
  font-family: "Rajdhani", sans-serif;
  margin-bottom: 30px;
}

.filter-toggle {
  display: none;
}

.filter-section {
  margin-bottom: 28px;
}

.filter-section:last-of-type {
  margin-bottom: 24px;
}

.section-title {
  font-family: "Rajdhani", sans-serif;
  font-size: 20px;
  font-weight: 700;
  color: #111827;
  margin: 0 0 16px 0;
  padding-bottom: 12px;
  border-bottom: 1px solid #e5e7eb;
}

.options-container {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.option-item {
  display: flex;
  align-items: center;
  padding: 8px 12px;
  border-radius: 6px;
  cursor: pointer;
}

.radio-input {
  width: 18px;
  height: 18px;
  margin: 0 12px 0 0;
  cursor: pointer;
  accent-color: #dc2626;
}

.option-label {
  font-family: "Rajdhani", sans-serif;
  font-size: 16px;
  font-weight: 500;
  color: #374151;
  cursor: pointer;
  user-select: none;
}

.radio-input:checked + .option-label {
  color: #dc2626;
  font-weight: 600;
}

.clear-button {
  width: 100%;
  padding: 12px 16px;
  background: #ffffff;
  border: 1px solid #e5e7eb;
  border-radius: 6px;
  font-family: "Rajdhani", sans-serif;
  font-size: 16px;
  font-weight: 600;
  color: #374151;
  cursor: pointer;
}

/* Focus states for accessibility */
.radio-input:focus {
  outline: 2px solid #dc2626;
  outline-offset: 2px;
}

.clear-button:focus {
  outline: 2px solid #dc2626;
  outline-offset: 2px;
}

/* Responsive design */
@media (max-width: 768px) {
  .filter-panel {
    max-width: 100%;
    margin: 0;
    border-radius: 8px;
    padding: 20px;
    box-sizing: border-box;
    right: 0;
    top: 0;
  }

  .section-title {
    font-size: 18px;
  }

  .option-label {
    font-size: 15px;
  }

  .filter-toggle {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    padding: 12px 16px;
    border: 1px solid #e5e7eb;
    border-radius: 6px;
    background: #ffffff;
    color: #111827;
    font-family: "Rajdhani", sans-serif;
    font-size: 18px;
    font-weight: 700;
    cursor: pointer;
  }

  .filter-toggle-icon {
    font-size: 24px;
    line-height: 1;
    transition: transform 0.2s ease;
  }

  .filter-toggle-icon.expanded {
    transform: rotate(180deg);
  }

  .filter-content {
    display: none;
    padding-top: 20px;
  }

  .filter-content.expanded {
    display: block;
  }
}
</style>
