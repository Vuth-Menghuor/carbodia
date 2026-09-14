<template>
  <div class="container">
    <div class="menu">
      <header class="header">
        <div class="description-logo">
          <div class="head">
            <div class="img">
              <img
                src="@/assets/images/media/carbodiaWhite.png"
                alt="Carbodia Logo"
              />
            </div>
            <div class="brand-name">Carbodia</div>
          </div>
          <div class="description">
            Your trusted platform for luxury and performance vehicles. Discover
            premium cars with detailed specifications, competitive pricing, and
            exceptional customer service. Browse our collection and find your
            dream car today.
          </div>
        </div>
        <nav class="nav">
          <ul>
            <li class="nav-column">
              <p class="nav-title">ABOUT</p>
              <span>Our Story</span>
              <span>Mission and Vision</span>
              <span>Achievements</span>
              <span>Partnerships</span>
            </li>
            <li class="nav-column">
              <p class="nav-title">PRODUCTS</p>
              <span>Product Categories</span>
              <span>Featured Products</span>
              <span>Filter and Search</span>
              <span>Special Offers</span>
            </li>
            <li class="nav-column">
              <p class="nav-title">BLOG</p>
              <span>Categories</span>
              <span>Featured Posts</span>
              <span>Subscribe to our Blog</span>
            </li>
            <li class="nav-column">
              <p class="nav-title">CONTACTS</p>
              <div class="contact">
                <Phone />
                <span>+855 69 552 601</span>
              </div>
              <div class="contact">
                <Email />
                <span>Carbodia168@gmail.com</span>
              </div>
            </li>
          </ul>
        </nav>
      </header>
    </div>
    <hr />
    <div class="footer">
      <div class="social-links">
        <a
          href="https://www.facebook.com/papapainkh/"
          target="_blank"
          rel="noopener noreferrer"
          aria-label="Facebook"
        >
          <Facebook />
        </a>
        <Instagram />
        <Tiktok />
      </div>
      <p class="copyright">
        Copyright © 2024 Carbodia, Ltd. All rights reserved.
      </p>
      <p class="legal-links">
        <span class="link-item">Privacy Policy</span>
        <span class="separator">|</span>
        <span class="link-item">Terms & Conditions</span>
      </p>
    </div>
  </div>
</template>
<style scoped>
.brand-name {
  font-family: "Goldman", sans-serif;
  font-size: 32px;
  font-weight: 400;
}

.container {
  background-color: #1e1e1e;
  padding: 60px 100px 40px 100px;
  width: 100%;
  box-sizing: border-box;
}

.head {
  display: flex;
  align-items: center;
  color: #ffffff;
  gap: 24px;
  margin-bottom: 24px;
}

.img {
  width: 80px;
  height: 60px;
}

.img img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.header {
  display: flex;
  justify-content: flex-start;
  align-items: flex-start;
  color: #ffffff;
  font-family: "Rajdhani", sans-serif;
  gap: 80px;
}

.description-logo {
  display: flex;
  flex-direction: column;
  max-width: 450px;
  flex-shrink: 0;
}

.description {
  color: #d1d5db;
  font-size: 15px;
  line-height: 1.8;
  font-family: "Rajdhani", sans-serif;
  font-weight: 400;
}

.nav ul {
  display: flex;
  list-style: none;
  gap: 50px;
  margin: 0;
  padding: 0;
}

.nav-column {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.nav-title {
  font-family: "Goldman", sans-serif;
  font-size: 16px;
  font-weight: 700;
  color: #ffffff;
  margin: 0 0 8px 0;
  letter-spacing: 0.5px;
}

.nav-column span {
  font-family: "Rajdhani", sans-serif;
  font-size: 15px;
  font-weight: 400;
  color: #d1d5db;
  cursor: pointer;
  white-space: nowrap;
}

.contact {
  display: flex;
  align-items: center;
  gap: 10px;
  color: #d1d5db;
}

hr {
  border: none;
  border-top: 1px solid #374151;
  margin: 40px 0 30px 0;
}

.footer {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 16px;
  font-family: "Rajdhani", sans-serif;
  color: #d1d5db;
}

.social-links {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 24px;
}

.social-links a {
  display: flex;
  align-items: center;
  text-decoration: none;
}

.copyright {
  font-size: 15px;
  margin: 0;
  color: #9ca3af;
}

.legal-links {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 15px;
  margin: 0;
}

.link-item {
  cursor: pointer;
  color: #d1d5db;
}

.separator {
  color: #6b7280;
}

@media (max-width: 1100px) {
  .container {
    padding: 52px 48px 36px;
  }

  .header {
    gap: 48px;
  }

  .nav ul {
    gap: 32px;
    flex-wrap: wrap;
  }
}

@media (max-width: 768px) {
  .container {
    padding: 40px 24px 28px;
  }

  .header {
    flex-direction: column;
    gap: 36px;
  }

  .description-logo {
    max-width: 620px;
  }

  .nav,
  .nav ul {
    width: 100%;
  }

  .nav ul {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 32px 24px;
  }

  .nav-column {
    gap: 10px;
    min-width: 0;
  }

  .nav-column span {
    white-space: normal;
  }

  hr {
    margin: 32px 0 24px;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 32px 16px 24px;
  }

  .head {
    gap: 14px;
    margin-bottom: 16px;
  }

  .img {
    width: 56px;
    height: 44px;
  }

  .brand-name {
    font-size: 26px;
  }

  .description,
  .nav-column span,
  .copyright,
  .legal-links {
    font-size: 14px;
  }

  .nav ul {
    gap: 28px 16px;
  }

  .nav-title {
    font-size: 14px;
  }

  .contact {
    gap: 8px;
  }

  .footer {
    gap: 14px;
    text-align: center;
  }

  .social-links {
    gap: 20px;
  }

  .legal-links {
    justify-content: center;
    flex-wrap: wrap;
    gap: 6px 10px;
  }
}
</style>
<script>
import Email from "./icons/footerIcons/Email.vue";
import Facebook from "./icons/footerIcons/Facebook.vue";
import Instagram from "./icons/footerIcons/Instagram.vue";
import Phone from "./icons/footerIcons/Phone.vue";
import Tiktok from "./icons/footerIcons/Tiktok.vue";
export default {
  components: {
    Facebook,
    Instagram,
    Tiktok,
    Phone,
    Email,
  },
};
</script>
