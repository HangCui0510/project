<template>
  <div class="login-page" :style="{ backgroundImage: 'url(' + backgroundUrl + ');' }">
    <div class="login-box">
      <div class="login-box__left">
        <div class="signinform">
          <v-form>
            <div class="text">
              <h4 :class="{ active: isLogin }" @click="isLogin = true">Log in</h4>
              <div class="flex-break" />
              <h4 :class="{ active: !isLogin }" @click="isLogin = false">Sign up</h4>
            </div>
            <v-text-field
              v-if="!isLogin"
              v-model="name"
              class="marginAdjust"
              label="Your Name"
              :rules="[
                val => (val && val.length > 0) || 'Please type your name'
              ]"
            />
            <v-text-field
              v-model="email"
              v-bind:class="{ marginAdjust: isLogin }"
              label="Your Email"
              lazy-rules
              :rules="[
                val => (val && val.length > 0) || 'Please type your email'
              ]"
            />
            <v-text-field
              v-model="password"
              label="Password"
              :rules="[
                val =>
                  (val !== null && val !== '') || 'Please type your password'
              ]"
            />
            <div class="labelAdjust">
              <input type="checkbox" id="checkbox" v-model="accept" />
              <label
                for="checkbox"
                class="v-label theme--light"
                style="left: 10px; right: auto; position:relative"
              >I accept the liciense and terms</label>
            </div>
            <div class="text marginAdjust">
              <v-btn color="success" @click="onSubmit">Submit</v-btn>
              <div class="flex-break" />
              <v-btn tile outlined color="error" @click="onReset">Reset</v-btn>
            </div>
          </v-form>
        </div>
      </div>
      <div class="login-box__right"></div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import router from "../router/index";
export default Vue.extend({
  name: "LoginPage",
  data() {
    return {
      email: "",
      password: "",
      name: "",
      accept: false,
      isLogin: true,
      router
    };
  },
  methods: {
    onSubmit() {
      if (
        this.email === "a@a.com" &&
        this.password == "password" &&
        this.accept == true
      ) {
        // eslint-disable-next-line @typescript-eslint/no-empty-function
        this.$router.replace({ path: "/" }).catch(() => {});
      } else if (this.accept == false) {
        this.$notify({
          group: "auth",
          type: "warn",
          title: "Important Message",
          duration: 1000,
          text: "You need to accept the license and terms first"
        });
      } else {
        this.$notify({
          group: "auth",
          type: "error",
          title: "Important Message",
          duration: 1000,
          text: "Incorrect username or password"
        });
      }
    },
    onReset() {
      this.email = "";
      this.password = "";
      this.name = "";
      this.accept = false;
    }
  }
});
</script>

<style lang="scss" scoped>
.buttonColor {
  color: rgba(255, 0, 0, 0.5);
}
.labelAdjust {
  margin-top: 15px;
}
.flex-break {
  margin-left: 30px;
}
.marginAdjust {
  margin-top: 20px;
}
.login-page {
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: url(./images/bgi.jpg);
  background-repeat: no-repeat;
  background-size: cover;
  width: 100vw;
  height: 100vh;
  .login-box {
    display: flex;
    width: 60%;
    height: 60%;
    justify-content: center;
    align-items: center;
    &__left {
      display: flex;
      width: 40%;
      height: 100%;
      justify-content: center;
      align-items: center;
      background: yellow;
      .signinform {
        margin-right: 20%;
        margin-left: 20%;
        height: 70%;
        width: 100%;
        .text {
          display: flex;
          h4 {
            color: grey;
            font-size: 24px;
          }
          h4.active {
            font-weight: 800;
            color: black;
          }
        }
      }
    }
    &__right {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 60%;
      height: 100%;
      background: blue;
    }
  }
}
</style>
