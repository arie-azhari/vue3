<template>
  <div class="w-full h-screen overflow-hidden bg-black text-gray-300">
    <Splash v-if="isShowSplash" />
    <Login v-if="!isShowSplash && isShowLogin" :handleEnter="handleEnter" />
    <home v-if="isShowHome" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { Splash, Login, Home } from "./components";
export default defineComponent({
  name: "App",
  components: {
    Splash,
    Login,
    Home,
  },
  data() {
    return {
      isShowSplash: false,
      isShowLogin: false,
      isShowHome: false,
    };
  },
  created() {
    this.handleSplash();
  },
  methods: {
    handleSplash() {
      const isFirstTime = localStorage.getItem("splash") === null;
      const isLogin = localStorage.getItem("login") === null;
      if (isFirstTime) {
        this.isShowSplash = true;
        setTimeout(() => {
          this.isShowSplash = false;
          this.isShowLogin = true;
        }, 5000);
      }
      if (!isFirstTime && isLogin) {
        this.isShowSplash = false;
        this.isShowLogin = true;
        this.isShowHome = false;
      }
      if (!isFirstTime && !isLogin) {
        this.isShowSplash = false;
        this.isShowLogin = false;
        this.isShowHome = true;
      }
    },
    handleEnter() {
      this.isShowSplash = false;
      this.isShowLogin = false;
      this.isShowHome = true;
      localStorage.setItem("login", "true");
    },
  },
});
</script>
