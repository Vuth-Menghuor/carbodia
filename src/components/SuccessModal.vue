<template>
  <div class="success-modal-overlay">
    <div class="success-card">
      <!-- Success Icon -->
      <div class="success-icon">
        <div class="checkmark-wrapper">
          <img
            :src="alienIcon"
            alt="Success Alien"
            class="success-alien-icon"
            data-v-inspector="src/components/SuccessModal.vue:7:11"
            data-v-30ab4535=""
          />
          <div class="success-animation">
            <div class="success-sparkle sparkle-1">✨</div>
            <div class="success-sparkle sparkle-2">⭐</div>
            <div class="success-sparkle sparkle-3">✨</div>
          </div>
        </div>
      </div>

      <!-- Content -->
      <div class="success-content">
        <h1 class="success-title">Purchase Complete</h1>
        <p class="success-subtitle">Your dream car is now yours</p>

        <div class="success-details">
          <div class="detail-item">
            <div class="detail-icon">
              <svg
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
              >
                <circle cx="12" cy="12" r="10" />
                <path d="m9 12 2 2 4-4" />
              </svg>
            </div>
            <span>Vehicle reserved successfully</span>
          </div>
          <div class="detail-item">
            <div class="detail-icon">
              <svg
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
              >
                <rect x="3" y="3" width="18" height="18" rx="2" ry="2" />
                <path d="m9 12 2 2 4-4" />
              </svg>
            </div>
            <span>Keys ready for pickup</span>
          </div>
        </div>
      </div>

      <!-- Actions -->
      <div class="success-actions">
        <button class="btn-primary" @click="handleContinue">
          <span>Continue Shopping</span>
          <svg
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <path d="m9 18 6-6-6-6" />
          </svg>
        </button>
        <button class="btn-secondary" @click="viewOrder">
          View Order Details
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import alienIcon from "@/assets/images/cute-alien-amico.svg";
export default {
  name: "SuccessModal",
  data() {
    return {
      alienIcon,
    };
  },
  methods: {
    handleContinue() {
      this.$router.push({ name: "home" });
    },
    viewOrder() {
      // Navigate to order details or user profile
      this.$router.push({ name: "user-profile" });
    },
  },
};
</script>

<style scoped>
.success-alien-icon {
  width: 100px;
  height: 100px;
  object-fit: contain;
  animation:
    scaleIn 0.5s ease-out 0.2s both,
    bounce 0.6s ease-out 0.8s both;
}
.success-modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(4px);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  padding: 20px;
  animation: fadeIn 0.3s ease-out;
}

.success-card {
  background: white;
  border-radius: 20px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
  overflow: hidden;
  max-width: 520px;
  width: 100%;
  animation: slideUp 0.4s ease-out;
}

/* Success Icon */
.success-icon {
  display: flex;
  justify-content: center;
  padding: 40px 30px 20px;
}

.checkmark-wrapper {
  width: 80px;
  height: 80px;
  /* border-radius: 50%; */
  display: flex;
  align-items: center;
  justify-content: center;
  animation:
    scaleIn 0.5s ease-out 0.2s both,
    bounce 0.6s ease-out 0.8s both;
  position: relative;
  overflow: visible;
}

.success-animation {
  position: absolute;
  top: -10px;
  left: -10px;
  right: -10px;
  bottom: -10px;
  pointer-events: none;
}

.success-sparkle {
  position: absolute;
  font-size: 16px;
  animation: sparkleFloat 2s ease-in-out infinite;
}

.sparkle-1 {
  top: -5px;
  left: 10px;
  animation-delay: 0s;
}

.sparkle-2 {
  top: 5px;
  right: -5px;
  animation-delay: 0.5s;
}

.sparkle-3 {
  bottom: -5px;
  left: 20px;
  animation-delay: 1s;
}

.checkmark {
  width: 32px;
  height: 32px;
}

.checkmark-circle {
  stroke: white;
  stroke-width: 3;
  fill: none;
  stroke-dasharray: 166;
  stroke-dashoffset: 166;
  animation: stroke 0.6s cubic-bezier(0.65, 0, 0.45, 1) forwards;
}

.checkmark-check {
  stroke: white;
  stroke-width: 3;
  stroke-dasharray: 48;
  stroke-dashoffset: 48;
  animation: stroke 0.3s cubic-bezier(0.65, 0, 0.45, 1) 0.8s forwards;
}

/* Content */
.success-content {
  padding: 0 40px 30px;
  text-align: center;
}

.success-title {
  margin: 0 0 8px 0;
  font-size: 28px;
  font-weight: 700;
  color: #1f2937;
  letter-spacing: -0.5px;
}

.success-subtitle {
  margin: 0 0 32px 0;
  font-size: 16px;
  color: #6b7280;
  font-weight: 400;
}

.success-details {
  display: flex;
  flex-direction: column;
  gap: 16px;
  margin-bottom: 32px;
}

.detail-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 16px;
  background: #f8fafc;
  border-radius: 12px;
  border: 1px solid #e5e7eb;
}

.detail-icon {
  width: 22px;
  height: 22px;
  color: #6b7280;
  flex-shrink: 0;
}

.detail-icon svg {
  width: 100%;
  height: 100%;
}

.detail-item span {
  font-size: 14px;
  color: #374151;
  font-weight: 500;
}

/* Actions */
.success-actions {
  padding: 0 40px 40px;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.btn-primary,
.btn-secondary {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 16px 24px;
  border: none;
  border-radius: 12px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s ease;
  text-decoration: none;
  min-height: 56px;
}

.btn-primary {
  background: linear-gradient(135deg, #2d5ea8, #2d5ea8);
  color: white;
}

.btn-primary svg {
  width: 20px;
  height: 20px;
}

.btn-secondary {
  background: white;
  color: #374151;
  border: 2px solid #e5e7eb;
}

.btn-secondary:hover {
  background: #f9fafb;
  border-color: #d1d5db;
}

/* Animations */
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(20px) scale(0.95);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

@keyframes scaleIn {
  from {
    opacity: 0;
    transform: scale(0.8);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

@keyframes stroke {
  to {
    stroke-dashoffset: 0;
  }
}

@keyframes bounce {
  0%,
  20%,
  50%,
  80%,
  100% {
    transform: scale(1);
  }
  40% {
    transform: scale(1.1);
  }
  60% {
    transform: scale(1.05);
  }
}

@keyframes sparkleFloat {
  0%,
  100% {
    opacity: 0;
    transform: translateY(0) scale(0.8) rotate(0deg);
  }
  50% {
    opacity: 1;
    transform: translateY(-10px) scale(1.2) rotate(180deg);
  }
}

/* Responsive */
@media (max-width: 480px) {
  .success-modal-overlay {
    padding: 16px;
  }

  .success-card {
    max-width: none;
    width: calc(100% - 32px);
  }

  .success-content,
  .success-actions {
    padding-left: 24px;
    padding-right: 24px;
  }

  .success-title {
    font-size: 24px;
  }

  .success-actions {
    padding-bottom: 24px;
  }
}
</style>
