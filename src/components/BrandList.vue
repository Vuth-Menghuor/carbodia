<template>
  <div class="product-list">
    <h3 class="header-product">Brand lists</h3>
    <div class="carousel-container">
      <div class="carousel-wrapper">
        <div class="product-container">
          <RouterLink
            class="RouterLink"
            v-for="(brand, index) in brands"
            :key="index"
          :to="`/brand/${brand.name}`"
        >
          <div class="product-item">
              <div class="brand-logo-slot">
                <img :src="brand.logo" :alt="brand.name" loading="lazy" />
              </div>
              <p class="branch-name">{{ brand.name }}</p>
            </div>
          </RouterLink>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      brands: [
        {
          name: "porsche",
          logo: new URL("@/assets/images/brands/porsche.png", import.meta.url)
            .href,
        },
        {
          name: "ferrari",
          logo: new URL("@/assets/images/brands/ferrari.png", import.meta.url)
            .href,
        },
        {
          name: "mercedes",
          logo: new URL("@/assets/images/brands/mercedes.png", import.meta.url)
            .href,
        },
        {
          name: "lamborghini",
          logo: new URL(
            "@/assets/images/brands/lamborghini.png",
            import.meta.url
          ).href,
        },
        {
          name: "bmw",
          logo: new URL("@/assets/images/brands/bmw.png", import.meta.url).href,
        },
      ],
    };
  },
  computed: {},
};
</script>
<style>
@import url("https://fonts.cdnfonts.com/css/yapari-trial");
@import url("https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap");

.header-product {
  padding: 80px 0px 40px 0px;
  font-family: "Rajdhani", sans-serif;
  font-weight: 600;
  font-size: 42px;
  color: #333;
  text-align: center;
  margin: 0;
  letter-spacing: -0.5px;
}

.product-list {
  text-align: center;
  margin: 40px 0;
  padding: 0 20px;
}

.carousel-container {
  max-width: 1200px;
  margin: 0 auto;
}

.carousel-wrapper {
  width: 100%;
  border-radius: 16px;
}

.product-container {
  display: grid;
  grid-template-columns: repeat(5, minmax(0, 1fr));
  gap: 20px;
  padding: 20px;
  width: 100%;
  box-sizing: border-box;
}

.RouterLink {
  min-width: 0;
  text-decoration: none;
}

.product-item {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  text-align: center;
  background: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
  border: 2px solid #e9ecef;
  border-radius: 8px;
  padding: 20px 60px;
  min-height: 90px;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
  box-sizing: border-box;
  min-width: 0;
  width: 100%;
}

.product-item::before {
  content: "";
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.4),
    transparent
  );
  transition: left 0.5s;
}

.product-item:hover {
  transform: translateY(-8px);
}

.product-item:hover::before {
  left: 100%;
}

.product-item img {
  max-width: 80px;
  max-height: 60px;
  object-fit: contain;
  filter: grayscale(20%);
  transition: all 0.3s ease;
  margin: 0;
}

.brand-logo-slot {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 64px;
}

.product-item:hover img {
  filter: grayscale(0%);
  transform: scale(1.1);
}

.branch-name {
  margin: 12px 0 0;
  font-size: 16px;
  font-family: "Rajdhani", sans-serif;
  font-weight: 500;
  color: #495057;
  text-transform: capitalize;
  letter-spacing: 0.5px;
  overflow-wrap: anywhere;
}

/* Tablet responsive */
@media (max-width: 1024px) {
  .product-container {
    grid-template-columns: repeat(3, minmax(0, 1fr));
  }

  .product-item {
    padding: 20px 24px;
  }
}

/* Mobile responsive */
@media (max-width: 768px) {
  .header-product {
    font-size: 32px;
    padding: 60px 0px 30px 0px;
  }

  .product-container {
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 20px;
  }

  .product-item {
    padding: 20px 30px;
    min-height: 80px;
  }

  .product-item img {
    max-width: 70px;
    max-height: 50px;
  }

  .carousel-arrow {
    width: 40px;
    height: 40px;
  }

  .brand-logo-slot {
    height: 54px;
  }

  .RouterLink:last-child:nth-child(odd) {
    grid-column: 1 / -1;
    justify-self: center;
    width: calc((100% - 20px) / 2);
  }
}

@media (max-width: 480px) {
  .header-product {
    font-size: 28px;
    padding: 50px 0px 25px 0px;
  }

  .product-container {
    gap: 15px;
    padding: 15px;
  }

  .product-item {
    padding: 15px 12px;
    min-height: 70px;
    border-radius: 8px;
  }

  .product-item img {
    max-width: 60px;
    max-height: 45px;
    margin-bottom: 10px;
  }

  .branch-name {
    font-size: 14px;
  }
}
</style>
