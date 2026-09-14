<template>
  <div class="back-button">
    <ChevronBack />
    <button @click="$router.back()">Back</button>
  </div>
</template>

<script>
import ChevronBack from "../icons/productPage/chevronBack.vue";

export default {
  components: {
    ChevronBack,
  },
};
</script>

<style scoped>
.back-button {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  display: flex;
  align-items: center;
  gap: 8px;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  padding: 18px 16px;
  width: 100%;
  box-sizing: border-box;
  cursor: pointer;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  z-index: 100;
}

.back-button button {
  font-family: "Rajdhani", sans-serif;
  font-size: 20px;
  font-weight: 600;
  color: #333;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
}

.back-button :deep(svg) {
  width: 32px;
  height: 32px;
  flex-shrink: 0;
}

.back-button :deep(svg path) {
  fill: #333;
}

@media (max-width: 480px) {
  .back-button {
    padding: 12px 14px;
  }

  .back-button button {
    font-size: 18px;
  }

  .back-button :deep(svg) {
    width: 26px;
    height: 26px;
  }
}
</style>
