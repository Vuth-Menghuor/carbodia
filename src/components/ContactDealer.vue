<script>
import Facebook from "./icons/contactDealer/facebook.vue";
import Instagram from "./icons/contactDealer/instagram.vue";
import Phone from "./icons/contactDealer/phone.vue";
export default {
  components: {
    Phone,
    Facebook,
    Instagram,
  },
};
</script>

<template>
  <h2>Contact the Dealer</h2>
  <div class="wrapper">
    <div class="header">
      <img src="@/assets/images/user.jpg" alt="please input the image" />
      <div class="dealer-name">
        <span>Daro Cars</span>
        <p>30 year old with Cars Edition</p>
      </div>
    </div>
    <div class="body">
      <button>
        <Phone />
        <span>Call +(855) 999 777 888</span>
      </button>
      <button>
        <Facebook />
        <span>Facebook</span>
      </button>
      <button>
        <Instagram />
        <span>Instagram</span>
      </button>
    </div>
    <div class="footer">
      <input type="text" placeholder="Type something..." />
      <div class="body">
        <button class="btn-contact">Contact Agent</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
h2 {
  font-family: "Rajdhani", sans-serif;
  font-weight: 700;
  font-size: 28px;
  color: #111827;
  margin-bottom: 20px;
}

.wrapper {
  border: 1px solid #e5e7eb;
  background-color: #ffffff;
  border-radius: 8px;
  width: 100%;
  max-width: 407px;
  padding: 24px;
  box-sizing: border-box;
}

.header {
  display: flex;
  align-items: center;
  gap: 16px;
  padding-bottom: 20px;
  border-bottom: 1px solid #e5e7eb;
}

.header > img {
  border: 1px solid #e5e7eb;
  border-radius: 50%;
  height: 56px;
  width: 56px;
  object-fit: cover;
}

.dealer-name {
  font-family: "Rajdhani", sans-serif;
}

.dealer-name > span {
  font-family: "Rajdhani", sans-serif;
  font-weight: 700;
  font-size: 20px;
  color: #111827;
  display: block;
  margin-bottom: 4px;
}

.dealer-name > p {
  font-family: "Rajdhani", sans-serif;
  font-size: 14px;
  color: #6b7280;
  margin: 0;
}

.body {
  padding: 20px 0;
}

.body > button {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  border: 1px solid #e5e7eb;
  background-color: #ffffff;
  height: 48px;
  width: 100%;
  margin-bottom: 12px;
  border-radius: 6px;
  cursor: pointer;
  font-family: "Rajdhani", sans-serif;
  font-size: 16px;
  font-weight: 500;
  color: #111827;
}

.body > button:last-child {
  margin-bottom: 0;
}

button > span {
  font-family: "Rajdhani", sans-serif;
  font-size: 16px;
  font-weight: 500;
}

.footer {
  border-top: 1px solid #e5e7eb;
  padding-top: 20px;
}

.footer > input {
  padding: 12px;
  width: 100%;
  font-family: "Rajdhani", sans-serif;
  font-size: 16px;
  border: 1px solid #e5e7eb;
  border-radius: 6px;
  outline: none;
  background-color: #f9fafb;
  color: #111827;
  margin-bottom: 12px;
  height: 100px;
  box-sizing: border-box;
  resize: none;
}

input:focus {
  border: 1px solid #dc2626;
  background-color: #ffffff;
}

.btn-contact {
  font-family: "Rajdhani", sans-serif;
  font-weight: 600;
  font-size: 16px;
  background-color: #dc2626;
  color: #ffffff;
  border: none;
  height: 48px;
  width: 100%;
  border-radius: 6px;
  cursor: pointer;
}

@media (max-width: 480px) {
  h2 {
    font-size: 24px;
    margin-bottom: 16px;
  }

  .wrapper {
    padding: 16px;
  }

  .header {
    gap: 12px;
  }

  .dealer-name > p {
    line-height: 1.35;
  }
}
</style>
