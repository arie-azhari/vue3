<template>
  <div class="w-full h-full flex justify-center items-center">
    <div class="space-y-8 flex flex-col items-center">
      <div class="flex space-x-8 items-center">
        <img class="w-32 h-32" src="@/assets/png/ubuntu.png" alt="" />
        <p class="text-7xl text-gray-300">ubuntu</p>
      </div>
      <div class="flex justify-center gap-8 w-full">
        <div
          v-for="(item, index) in loading"
          :key="index"
          class="h-3 w-3 rounded-full"
          :class="
            !item
              ? 'bg-white  duration-500'
              : 'bg-red-600 border border-yellow-500 duration-500'
          "
        />
      </div>
    </div>
  </div>
</template>
<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "Splash",
  data() {
    return {
      interval: null,
      loading: [false, false, false, false, false],
    };
  },
  created() {
    this.changeLoading();
    localStorage.setItem("splash", true);
  },
  unmounted() {
    clearInterval(this.interval);
  },
  methods: {
    changeLoading() {
      this.interval = setInterval(() => {
        const idx = this.loading.findIndex((val) => val == true);
        if (idx === -1) {
          this.loading[0] = true;
        } else if (idx + 1 === this.loading.length) {
          this.loading = [false, false, false, false, false];
        } else {
          this.loading = [false, false, false, false, false];
          this.loading[idx + 1] = true;
        }
      }, 700);
    },
  },
});
</script>
