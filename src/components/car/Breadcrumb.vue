<template>
  <!-- <NavComponent /> -->
  <nav class="nav-link">
    <RouterLink to="/">
      <li>
        <a href="">Home</a>
        <ChevronRight />
      </li>
    </RouterLink>
    <RouterLink
      :to="{ name: 'brand', params: { brandName: brand.toLowerCase() } }"
    >
      <li>
        <a href="">{{ brand }}</a>
        <ChevronRight />
      </li>
    </RouterLink>
    <li>
      <a href="">{{ model }}</a>
      <ChevronRight />
    </li>
  </nav>
</template>
<script>
import { mapState } from "pinia";
import ChevronRight from "../icons/NavIcons/chevronRight.vue";
import NavComponent from "../navigation/NavComponent.vue";
import { useCarStore } from "../../stores/cars";
export default {
  components: {
    ChevronRight,
    NavComponent,
  },
  props: {
    brand: String,
    model: String,
  },
};
</script>
<style scoped>
.nav-link {
  display: flex;
  gap: 20px;
  padding: 136px 136px 0 136px;
  box-sizing: border-box;
}

.nav-link li {
  display: flex;
  align-items: center;
  text-decoration: none;
  list-style: none;
  gap: 6px;
}

a {
  text-decoration: none;
  color: #717171;
  font-size: 18px;
}

@media (max-width: 1200px) {
  .nav-link {
    padding-left: 60px;
    padding-right: 60px;
  }
}

@media (max-width: 768px) {
  .nav-link {
    gap: 10px;
    padding: 100px 20px 0;
    overflow-x: auto;
    white-space: nowrap;
  }

  a {
    font-size: 16px;
  }
}

@media (max-width: 480px) {
  .nav-link {
    padding: 88px 16px 0;
  }
}
</style>
