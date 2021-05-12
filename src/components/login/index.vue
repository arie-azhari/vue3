<template>
  <div class="w-full h-full" @click="handleShowForm">
    <div class="background relative bg-cover w-full h-full">
      <div class="absolute p-2 z-10 w-full gap-3 flex justify-end">
        <img
          class="w-4 h-4 cursor-pointer"
          src="@/assets/svg/wifi.svg"
          alt=""
        />
        <img
          class="w-4 h-4 cursor-pointer"
          src="@/assets/svg/volume.svg"
          alt=""
        />
        <img
          class="w-4 h-4 cursor-pointer"
          src="@/assets/svg/battery.svg"
          alt=""
        />
      </div>
      <transition name="route" mode="out-in">
        <div
          v-if="!showForm"
          class="
            absolute
            p-2
            z-10
            w-full
            gap-3
            flex
            h-full
            top-1/3
            justify-center
          "
        >
          <div class="text-center space-y-4 text-white">
            <div class="text-8xl">
              {{ hour
              }}<span :class="isMs ? 'text-gray-300' : 'text-white'">:</span
              >{{ minute }}
            </div>
            <div>{{ date }}</div>
          </div>
        </div>
      </transition>
      <transition name="routein" mode="out-in">
        <div
          v-if="showForm"
          class="
            absolute
            p-2
            z-10
            w-full
            gap-3
            flex
            h-full
            top-1/3
            justify-center
          "
        >
          <div class="flex-col items-center gap-4 flex">
            <img
              class="w-24 h-24 p-4 rounded-full bg-opacity-40 bg-gray-500"
              src="@/assets/svg/user.svg"
              alt=""
            />
            <div class="font-medium text-xl">Arie Azhari</div>
            <div>
              <input
                autofocus
                v-model="password"
                type="password"
                class="px-4 py-1 text-black"
                placeholder="password"
              />
            </div>
          </div>
        </div>
      </transition>
      <div
        class="
          w-full
          h-full
          bg-black
          opacity-50
          flex
          justify-center
          items-center
        "
      />
    </div>
  </div>
</template>
<script>
import { defineComponent } from "vue";
import dayjs from "dayjs";
export default defineComponent({
  data() {
    return {
      interval: null,
      hour: "",
      minute: "",
      isMs: true,
      date: "Wednesday Mey 12",
      showForm: false,
      password: "",
    };
  },
  props: {
    handleEnter: Function,
  },
  mounted() {
    console.log("asd");
    this.interval = setInterval(() => {
      this.updateDiffs();
      this.isMs = !this.isMs;
    }, 1000);

    this.updateDiffs();
    window.addEventListener("keyup", (e) => {
      if (e.key == "Escape") {
        this.showForm = false;
        this.password = "";
      } else if (e.key == "Enter" && this.password !== "") {
        console.log("login");
        this.handleEnter();
      } else {
        this.showForm = true;
      }
    });
  },
  unmounted() {
    clearInterval(this.interval);
  },
  methods: {
    updateDiffs() {
      this.hour = dayjs().format("HH");
      this.minute = dayjs().format("mm");
      this.date = dayjs().format("dddd MMM DD");
    },
    handleShowForm() {
      this.showForm = true;
    },
  },
});
</script>
<style scoped>
.background {
  background-image: url("~@/assets/png/lock.png");
  height: "100%";
}

.route-enter-from,
.route-leave-to {
  opacity: 0;
  transform: translateY(-50px);
}
.route-enter-active,
.route-leave-active {
  transition: all 0.5s ease;
}
.route-enter-to,
.route-leave-from {
  opacity: 1;
  transform: translateY(0);
}

.routein-enter-from,
.routein-leave-to {
  opacity: 0;
  transform: translateY(50px);
}
.routein-enter-active,
.routein-leave-active {
  transition: all 0.5s ease;
}
.routein-enter-to,
.routein-leave-from {
  opacity: 1;
  transform: translateY(0);
}
</style>
