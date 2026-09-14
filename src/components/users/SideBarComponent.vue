<template>
  <div class="sidebar-container">
    <!-- Header Section -->
    <div class="sidebar-header">
      <div class="logo-section">
        <div class="logo-placeholder">
          <img
            src="@/assets/images/media/carbodiaWhite.png"
            alt="Carbodia Logo"
            class="logo-icon"
          />
        </div>
        <div class="brand-info">
          <span class="brand-name">Carbodia</span>
        </div>
      </div>
      <button @click="closeSidebar" class="close-button">
        <Icon icon="material-symbols:close" />
      </button>
    </div>

    <!-- Navigation Section -->
    <nav class="navigation">
      <div class="nav-group">
        <div class="nav-group-label">Main</div>

        <div
          class="nav-item active"
          @click="navigate('home')"
        >
          <Icon icon="material-symbols:dashboard-rounded" />
          <span>Dashboard</span>
        </div>

        <div class="nav-item" @click="navigate('bookmarks')">
          <Icon icon="material-symbols:bookmark-outline" />
          <span>Bookmarks</span>
        </div>

        <div class="nav-item">
          <Icon icon="material-symbols:inventory-2-outline" />
          <span>Products</span>
        </div>
      </div>

      <!-- Settings Group -->
      <div class="nav-group">
        <div class="nav-group-label">Settings</div>

        <div class="nav-item">
          <Icon icon="material-symbols:palette-outline" />
          <span>Appearance</span>
        </div>

        <div class="nav-item">
          <Icon icon="material-symbols:help-outline" />
          <span>Help & Support</span>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
import { Icon } from "@iconify/vue";

export default {
  name: "Sidebar",
  components: {
    Icon,
  },
  methods: {
    closeSidebar() {
      this.$emit("close-sidebar");
    },
    navigate(name) {
      this.$router.push({ name });
      this.closeSidebar();
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Manrope:wght@400;500;600;700&display=swap");

.sidebar-container {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
  width: 300px;
  height: 100dvh;
  background: #ffffff;
  display: flex;
  flex-direction: column;
  box-shadow: 2px 0 8px rgba(0, 0, 0, 0.1);
  font-family: "Rajdhani", -apple-system, BlinkMacSystemFont, sans-serif;
}

/* Header Section */
.sidebar-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 14px 24px;
  background: #f8f9fa;
  border-bottom: 1px solid #e9ecef;
}

.logo-section {
  display: flex;
  align-items: center;
  gap: 12px;
}

.logo-placeholder {
  width: 44px;
  height: 44px;
  background: #f8f9fa;
  border-radius: 50%;
  border: 1px solid #dc2626;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 6px;
}

.logo-icon {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.brand-info {
  display: flex;
  flex-direction: column;
}

.brand-name {
  font-family: "Goldman", sans-serif;
  font-weight: 700;
  font-size: 18px;
  background: linear-gradient(135deg, #dc2626, #b91c1c);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  line-height: 1.2;
}

.brand-subtitle {
  font-family: "Rajdhani", sans-serif;
  font-weight: 500;
  font-size: 13px;
  color: #6c757d;
  line-height: 1.2;
}

.close-button {
  background: #f8f9fa;
  border: 1px solid #dee2e6;
  cursor: pointer;
  padding: 8px;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #6c757d;
  outline: none;
  width: 44px;
  height: 44px;
}

.close-button:focus {
  outline: none;
}

/* Navigation Section */
.navigation {
  flex: 1;
  padding: 24px 0;
  overflow-y: auto;
  scrollbar-width: none;
  -ms-overflow-style: none;
}

.navigation::-webkit-scrollbar {
  display: none;
}

.nav-group {
  margin-bottom: 32px;
}

.nav-group:last-child {
  margin-bottom: 0;
}

.nav-group-label {
  font-family: "Rajdhani", sans-serif;
  font-weight: 600;
  font-size: 12px;
  background: linear-gradient(135deg, #dc2626, #b91c1c);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  padding: 0 24px;
  margin-bottom: 12px;
}

.nav-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 20px;
  margin: 0 16px 4px 16px;
  border-radius: 10px;
  font-family: "Rajdhani", sans-serif;
  font-weight: 500;
  font-size: 15px;
  color: #495057;
  cursor: pointer;
  position: relative;
}

.nav-item:hover {
  background: #f8f9fa;
  color: #dc2626;
}

.nav-item.active {
  background: #fef2f2;
  color: #dc2626;
  font-weight: 600;
}

.nav-item.active::before {
  content: "";
  position: absolute;
  left: -16px;
  top: 50%;
  transform: translateY(-50%);
  width: 3px;
  height: 24px;
  background: linear-gradient(135deg, #dc2626, #b91c1c);
  border-radius: 0 3px 3px 0;
}

.nav-badge {
  margin-left: auto;
  padding: 2px 8px;
  background: #e2e8f0;
  color: #718096;
  font-size: 11px;
  font-weight: 600;
  border-radius: 12px;
  min-width: 20px;
  text-align: center;
}

.nav-badge.new {
  background: linear-gradient(135deg, #48bb78 0%, #38a169 100%);
  color: white;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%,
  100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.05);
  }
}

/* Responsive Design */
@media (max-width: 768px) {
  .sidebar-container {
    width: min(72vw, 300px);
  }

  .nav-item {
    margin: 0 12px;
  }
}

@media (max-width: 480px) {
  .sidebar-header {
    padding: 12px 16px;
  }

  .navigation {
    padding: 20px 0 calc(24px + env(safe-area-inset-bottom));
  }

  .nav-group-label {
    padding: 0 20px;
  }

  .nav-item {
    min-height: 46px;
    margin: 0 10px 4px;
    padding: 10px 16px;
  }
}

/* Icon Styling */
.sidebar-container :deep(svg) {
  width: 20px;
  height: 20px;
  color: inherit;
}

/* Smooth transitions for all interactive elements */
* {
  transition: color 0.2s ease, background-color 0.2s ease, transform 0.2s ease;
}

/* Focus states for accessibility */
.nav-item:focus {
  outline: 2px solid #667eea;
  outline-offset: 2px;
}
</style>
