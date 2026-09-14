<template>
  <div class="header-content">
    <div class="logo-title">
      <img
        class="logo-img"
        src="@/assets/images/media/carbodiaWhite.png"
        alt="Carbodia Logo"
      />
      <span>Carbodia</span>
    </div>
    <div class="empty-space"></div>
    <div class="container-btn">
      <RouterLink to="/">
        <button class="login-direction">Go to website</button>
      </RouterLink>
      <RouterLink v-if="!isCreateForm" to="/signup" tag="button">
        <button>Sign Up</button>
      </RouterLink>
      <RouterLink v-else to="/login" tag="button">
        <button>Sign in</button>
      </RouterLink>
    </div>
  </div>

  <!-- Log in  Section-->
  <div class="container">
    <form v-if="!isCreateForm" class="form-sec" @submit.prevent>
      <div class="form-layout">
        <div class="head-sec">
          <h2 @click="signIn">Sign In</h2>
          <span
            >Don't have an account?
            <strong @click="changeForm">Sign Up</strong></span
          >
        </div>
        <div class="fill-email">
          <svg
            class="icon-style"
            width="20"
            height="20"
            viewBox="0 0 20 20"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              clip-rule="evenodd"
              d="M10 14.974L0 6.14899V17.5H20V6.14899L10 14.974ZM10.001 12.312L0 3.48102V2.5H20V3.48102L10.001 12.312Z"
              fill="black"
              fill-opacity="0.7"
            />
            fill="black" fill-opacity="0.7" />
          </svg>
          <input
            v-model="user.email"
            type="text"
            name="fill-input"
            class="fill-input"
            placeholder="Email"
          />
        </div>
        <div class="fill-pass">
          <svg
            class="icon-style"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M19 10H20C20.5523 10 21 10.4477 21 11V21C21 21.5523 20.5523 22 20 22H4C3.44772 22 3 21.5523 3 21V11C3 10.4477 3.44772 10 4 10H5V9C5 5.13401 8.13401 2 12 2C15.866 2 19 5.13401 19 9V10ZM17 10V9C17 6.23858 14.7614 4 12 4C9.23858 4 7 6.23858 7 9V10H17ZM11 14V18H13V14H11Z"
              fill="black"
              fill-opacity="0.7"
            />
            fill="black" fill-opacity="0.7" />
          </svg>
          <input
            v-model="user.password"
            type="password"
            name="fill-input"
            class="fill-input-password"
            placeholder="Password"
          />
        </div>
      </div>
      <div class="form-check">
        <div class="check-box">
          <input class="check-box-icon" type="checkbox" />
          <span>Remember me</span>
        </div>
        <span class="forget-ps">Forget Password?</span>
      </div>
      <div class="btn-sign-in"><button @click="signIn">Sign In</button></div>
      <div class="register">
        <hr />
        <span>or register with</span>
        <hr />
      </div>
      <div class="sign-with">
        <button>
          <GoogleLogin />
          Google
        </button>
        <button>
          <FacebookLogin />
          Facebook
        </button>
      </div>
    </form>

    <!-- Sign up Section-->
    <form v-else class="form-sec" @submit.prevent="onSubmit">
      <div class="form-layout">
        <div class="head-sec">
          <h2>Create an account</h2>
          <span
            >Don't have an account?
            <strong @click="changeForm">Sign In</strong></span
          >
        </div>
        <div class="fname-lname">
          <div class="fname">
            <input
              v-model="firstname"
              v-bind="firstnameProps"
              type="text"
              class="fill-fname-lname"
              placeholder="First Name"
            />
            <p class="text-error">{{ errors.firstname }}</p>
          </div>
          <div class="lname">
            <input
              v-model="lastname"
              v-bind="lastnameProps"
              type="text"
              class="fill-fname-lname"
              placeholder="Last Name"
            />
            <p class="text-error">{{ errors.lastname }}</p>
          </div>
        </div>
        <div class="fill-email">
          <svg
            class="icon-style"
            width="20"
            height="20"
            viewBox="0 0 20 20"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              clip-rule="evenodd"
              d="M10 14.974L0 6.14899V17.5H20V6.14899L10 14.974ZM10.001 12.312L0 3.48102V2.5H20V3.48102L10.001 12.312Z"
              fill="black"
              fill-opacity="0.7"
            />
          </svg>
          <input
            v-model="email"
            v-bind="emailProps"
            type="text"
            name="fill-input"
            class="fill-input"
            placeholder="Email"
          />
          <p class="text-error">{{ errors.email }}</p>
        </div>
        <div class="fill-pass">
          <svg
            class="icon-style"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M19 10H20C20.5523 10 21 10.4477 21 11V21C21 21.5523 20.5523 22 20 22H4C3.44772 22 3 21.5523 3 21V11C3 10.4477 3.44772 10 4 10H5V9C5 5.13401 8.13401 2 12 2C15.866 2 19 5.13401 19 9V10ZM17 10V9C17 6.23858 14.7614 4 12 4C9.23858 4 7 6.23858 7 9V10H17ZM11 14V18H13V14H11Z"
              fill="black"
              fill-opacity="0.7"
            />
          </svg>
          <input
            v-model="password"
            v-bind="passwordProps"
            type="password"
            name="fill-input"
            class="fill-input-password"
            placeholder="Password"
          />
          <p class="text-error">{{ errors.password }}</p>
        </div>
      </div>
      <div class="form-check">
        <div class="check-box">
          <input
            v-model="termsChecked"
            class="check-box-icon"
            type="checkbox"
          />
          <span>I agree to the</span>
          <strong>Terms & conditions</strong>
        </div>
      </div>
      <div class="btn-sign-up" :class="{ 'btn-disabled': !termsChecked }">
        <button>Sign Up</button>
      </div>
      <div class="register">
        <hr />
        <span>or register with</span>
        <hr />
      </div>
      <div class="sign-with">
        <button>
          <GoogleLogout />
          Google
        </button>
        <button>
          <FacebookLogout />
          Facebook
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import GoogleLogin from "@/components/icons/auth/GoogleLogin.vue";
import FacebookLogin from "@/components/icons/auth/FacebookLogin.vue";
import GoogleLogout from "@/components/icons/auth/GoogleLogout.vue";
import FacebookLogout from "@/components/icons/auth/FacebookLogout.vue";

import { useForm } from "vee-validate";
import { string } from "yup";

import pb from "../../lib/pocketbase";
export default {
  setup() {
    const emailValidator = string().required("Email is required").email();
    const passwordValidator = string()
      .required("Password is required")
      .min(8, "Password must be at least 8 characters");
    const firsnameValidator = string().required("First name is required");
    const lastnameValidator = string().required("Last name is required");

    const { defineField, handleSubmit, errors } = useForm({
      validationSchema: {
        email: emailValidator,
        password: passwordValidator,
        firstname: firsnameValidator,
        lastname: lastnameValidator,
      },
    });

    const [email, emailProps] = defineField("email");
    const [password, passwordProps] = defineField("password");
    const [firstname, firstnameProps] = defineField("firstname");
    const [lastname, lastnameProps] = defineField("lastname");

    const onSubmit = handleSubmit((values) => {
      console.log(values);
    });

    return {
      errors,
      onSubmit,
      email,
      emailProps,
      password,
      passwordProps,
      firstname,
      firstnameProps,
      lastname,
      lastnameProps,
    };
  },
  components: {
    GoogleLogin,
    FacebookLogin,
    GoogleLogout,
    FacebookLogout,
  },
  props: {
    isCreateForm: Boolean,
  },
  data() {
    return {
      isLoggedIn: false,
      skipItems: Array(5).fill(null),
      activeIndex: 0,
      termsChecked: false,
      user: {
        email: "",
        password: "",
      },
    };
  },
  methods: {
    changeForm() {
      this.$router.push(this.isCreateForm ? "/login" : "/signup");
    },
    async signIn() {
      try {
        pb.authStore.clear();
        const authData = await pb
          .collection("users")
          .authWithPassword(this.user.email, this.user.password);

        console.log(pb.authStore.record.avatar);

        if (pb.authStore.isValid) {
          this.$router.push({ name: "home" });
        }
      } catch (error) {
        alert(`Authentication failed: ${error}`);
      }
    },
    async createUser() {
      try {
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Rajdhani:wght@300;400;500;600;700&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&family=Noto+Sans:ital,wght@0,100..900;1,100..900&family=Roboto+Serif:ital,opsz,wght@0,8..144,100..900;1,8..144,100..900&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Goldman:wght@400;700&family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&family=Montserrat:ital,wght@0,100..900;1,100..900&family=Noto+Sans:ital,wght@0,100..900;1,100..900&family=Quattrocento+Sans:ital,wght@0,400;0,700;1,400;1,700&family=Roboto+Flex:opsz,wght@8..144,100..1000&family=Roboto+Serif:ital,opsz,wght@0,8..144,100..900;1,8..144,100..900&display=swap");
@import url("https://fonts.cdnfonts.com/css/yapari-trial");
@import url("https://fonts.googleapis.com/css2?family=Goldman:wght@400;700&family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&family=Montserrat:ital,wght@0,100..900;1,100..900&family=Noto+Sans:ital,wght@0,100..900;1,100..900&family=Roboto+Flex:opsz,wght@8..144,100..1000&family=Roboto+Serif:ital,opsz,wght@0,8..144,100..900;1,8..144,100..900&display=swap");

a {
  text-decoration: none;
  color: black;
}

* {
  font-family: "Rajdhani", sans-serif;
}

.container {
  position: fixed;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  background: url("@/assets/images/bg-authentication.jpg");
  background-size: cover;
  background-position: center;
  width: 100%;
  min-height: 100vh;
  min-height: 100dvh;
  box-sizing: border-box;
  overflow-y: auto;
  padding: 104px 24px 32px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.container form {
  position: relative;
  left: 0;
  margin: 0 auto;
}

.form-sec {
  height: auto;
  width: min(100%, 500px);
  box-sizing: border-box;
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-radius: 16px;
  padding: 40px 50px;
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  margin: 0 auto;
}

.form-layout {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.head-sec {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: "Rajdhani", sans-serif;
  text-align: center;
  line-height: 28px;
  padding-bottom: 30px;
  width: 100%;
}

h2 {
  font-size: 38px;
  font-weight: 600;
  margin-bottom: 10px;
  color: #ffffff;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.head-sec span {
  font-size: 16px;
  color: rgba(255, 255, 255, 0.9);
}

.head-sec strong {
  color: #ffffff;
  text-decoration: underline;
  cursor: pointer;
  font-weight: 600;
  transition: color 0.2s ease;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
}

.head-sec strong:hover {
  color: rgba(255, 255, 255, 0.8);
}

.fill-input {
  width: 100%;
  width: -webkit-fill-available;
  height: 45px;
  border: none;
  border-bottom: 2px solid rgba(255, 255, 255, 0.4);
  border-radius: 0;
  outline: none;
  font-family: "Rajdhani", sans-serif;
  font-size: 15px;
  padding: 0 15px 0 45px;
  transition: all 0.3s ease;
  background: transparent;
  color: #ffffff;
}

.fill-input::placeholder {
  color: rgba(255, 255, 255, 0.6);
}

.fill-input:focus {
  border-bottom-color: rgba(255, 255, 255, 0.9);
}

.fill-input-password {
  width: 100%;
  width: -webkit-fill-available;
  height: 45px;
  border: none;
  border-bottom: 2px solid rgba(255, 255, 255, 0.4);
  border-radius: 0;
  outline: none;
  font-family: "Rajdhani", sans-serif;
  font-size: 15px;
  padding: 0 15px 0 45px;
  transition: all 0.3s ease;
  background: transparent;
  color: #ffffff;
}

.fill-input-password::placeholder {
  color: rgba(255, 255, 255, 0.6);
}

.fill-input-password:focus {
  border-bottom-color: rgba(255, 255, 255, 0.9);
}

.fill-email input[type="text"] {
  padding-right: 15px;
}

.fill-pass input[type="password"] {
  padding-right: 15px;
}

.icon-style {
  position: absolute;
  cursor: pointer;
  margin-top: 12px;
  margin-left: 15px;
  opacity: 0.8;
  filter: brightness(0) invert(1);
}

.fill-email {
  padding-bottom: 25px;
  position: relative;
  width: 100%;
}

.fill-pass {
  padding-bottom: 20px;
  position: relative;
  width: 100%;
}

.form-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  font-size: 15px;
}

.forget-ps {
  cursor: pointer;
  color: rgba(255, 255, 255, 0.9);
  text-decoration: underline;
  transition: color 0.2s ease;
}

.forget-ps:hover {
  color: #ffffff;
}

.check-box {
  display: flex;
  align-items: center;
}

.check-box-icon {
  height: 18px;
  width: 18px;
  cursor: pointer;
  accent-color: #ffffff;
  filter: brightness(0) invert(1);
}

.check-box span {
  padding-left: 8px;
  font-size: 15px;
  color: rgba(255, 255, 255, 0.9);
}

.btn-sign-in {
  display: flex;
  justify-content: center;
  padding-top: 30px;
  width: 100%;
}

.btn-sign-up {
  display: flex;
  justify-content: center;
  margin-top: 30px;
  width: 100%;
}

.btn-sign-up button {
  height: 50px;
  width: 100%;
  border: none;
  background: rgba(255, 255, 255, 0.25);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-radius: 8px;
  color: white;
  font-family: "Rajdhani", sans-serif;
  font-size: 18px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.btn-sign-up button:hover {
  background: rgba(255, 255, 255, 0.35);
  border-color: rgba(255, 255, 255, 0.5);
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

.btn-sign-up button:active {
  background: rgba(255, 255, 255, 0.2);
  transform: translateY(0);
}

.btn-sign-in button {
  height: 50px;
  width: 100%;
  border: none;
  background: rgba(255, 255, 255, 0.25);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-radius: 8px;
  color: white;
  font-family: "Rajdhani", sans-serif;
  font-size: 18px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.btn-sign-in button:hover {
  background: rgba(255, 255, 255, 0.35);
  border-color: rgba(255, 255, 255, 0.5);
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

.btn-sign-in button:active {
  background: rgba(255, 255, 255, 0.2);
  transform: translateY(0);
}

.btn-disabled {
  cursor: not-allowed;
  opacity: 0.6;
}

.register {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 15px;
  margin: 25px 0;
  width: 100%;
}

.register hr {
  flex: 1;
  border: none;
  margin: 0;
  border-top: 1px solid rgba(255, 255, 255, 0.3);
}

.register span {
  font-size: 15px;
  color: rgba(255, 255, 255, 0.8);
}

.sign-with {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 15px;
  width: 100%;
}

.sign-with button {
  display: flex;
  align-items: center;
  justify-content: center;
  flex: 1;
  height: 45px;
  border-radius: 8px;
  border: 1px solid rgba(255, 255, 255, 0.3);
  background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(10px);
  cursor: pointer;
  font-size: 16px;
  font-weight: 500;
  color: white;
  transition: all 0.2s ease;
}

.sign-with button:hover {
  border-color: rgba(255, 255, 255, 0.5);
  background: rgba(255, 255, 255, 0.25);
  transform: translateY(-2px);
}

.icon {
  padding-right: 8px;
}

.fill-fname-lname {
  width: 100%;
  box-sizing: border-box;
  min-width: 0;
  height: 45px;
  border: none;
  border-bottom: 2px solid rgba(255, 255, 255, 0.4);
  border-radius: 0;
  outline: none;
  font-family: "Rajdhani", sans-serif;
  font-size: 15px;
  padding: 0 15px;
  transition: all 0.3s ease;
  background: transparent;
  color: #ffffff;
}

.fill-fname-lname::placeholder {
  color: rgba(255, 255, 255, 0.6);
}

.fill-fname-lname:focus {
  border-bottom-color: rgba(255, 255, 255, 0.9);
}

.fname-lname {
  display: flex;
  align-items: flex-start;
  gap: 20px;
  padding-bottom: 25px;
  width: 100%;
}

.fname input[type="text"] {
  padding-right: 0px;
}

.lname input[tpe="text"] {
  padding-right: 0px;
}

.fname {
  flex: 1;
  min-width: 0;
}

.lname {
  flex: 1;
  min-width: 0;
}

.check-box strong {
  text-decoration: underline;
  padding-left: 5px;
  font-family: "Rajdhani", sans-serif;
  font-size: 15px;
  color: #ffffff;
  cursor: pointer;
  font-weight: 600;
  transition: color 0.2s ease;
}

.check-box strong:hover {
  color: rgba(255, 255, 255, 0.8);
}

.header-content {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: auto;
  box-sizing: border-box;
  padding: 20px 40px;
  background-color: transparent;
  text-align: center;
  z-index: 10;
}

.empty-space {
  display: none;
}

.container-btn {
  display: flex;
  background-color: transparent;
  align-items: center;
  height: auto;
  padding: 0;
  width: auto;
  column-gap: 12px;
}

.container-btn::after {
  display: none;
}

.container-btn::before {
  display: none;
}

.container-btn .login-direction {
  position: relative;
}

.logo-img {
  height: 50px;
  width: auto;
}

.logo-title {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: transparent;
  height: auto;
  width: auto;
  padding: 0;
  column-gap: 15px;
}

.logo-title span {
  color: #ffffff;
  font-family: "Goldman", sans-serif;
  font-size: 28px;
  font-weight: 400;
  font-style: normal;
  transition: color 0.4s ease;
}

.logo-title::before {
  display: none;
}

.logo-title::after {
  display: none;
}

.header-content button {
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  height: 40px;
  padding: 0 20px;
  color: white;
  border-radius: 6px;
  font-weight: 500;
  font-family: "Rajdhani", sans-serif;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.2s ease, border-color 0.2s ease;
}

.header-content button:hover {
  background: rgba(255, 255, 255, 0.25);
  border-color: rgba(255, 255, 255, 0.5);
}

.footer-skip {
  position: absolute;
  left: -50%;
  margin-top: 40px;
  color: white;
  font-size: 24px;
  font-family: "Rajdhani", sans-serif;
  font-weight: normal;
}

.footer-skip {
  position: relative;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

.skip-form {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-top: 30px;
}

.indicator {
  width: 44px;
  height: 6px;
  border-radius: 10px;
  background-color: rgb(88, 88, 88);
  transition: all 0.3s ease-in-out;
}

.indicator-active {
  background-color: white;
}

.text-error {
  color: #e74c3c;
  font-size: 12px;
  margin-top: 5px;
  font-family: "Rajdhani", sans-serif;
}

@media (max-width: 600px) {
  .container {
    align-items: flex-start;
    padding: 88px 16px 24px;
  }

  .form-sec {
    padding: 32px 24px;
    border-radius: 12px;
  }

  .header-content {
    padding: 16px;
  }

  .logo-img {
    height: 40px;
  }

  .logo-title {
    column-gap: 10px;
  }

  .logo-title span {
    font-size: 23px;
  }

  .container-btn {
    column-gap: 8px;
  }

  .header-content button {
    height: 36px;
    padding: 0 12px;
    font-size: 13px;
  }

  h2 {
    font-size: 32px;
  }

  .head-sec {
    padding-bottom: 24px;
  }
}

@media (max-width: 430px) {
  .logo-title span {
    display: none;
  }

  .fname-lname {
    gap: 12px;
  }
}

@media (max-width: 360px) {
  .container {
    padding-inline: 12px;
  }

  .form-sec {
    padding: 28px 20px;
  }

  .form-check {
    align-items: flex-start;
    flex-direction: column;
    gap: 10px;
  }

  .sign-with {
    gap: 10px;
  }

  .register {
    gap: 10px;
  }

  .register span {
    white-space: nowrap;
  }
}
</style>
