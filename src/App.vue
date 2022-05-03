<template>
  <div id="app" class="p-10">
    <div class="flex flex-col">
      <input
        :value="this.activeDate ? this.activeDate : today"
        class="calendar-input cursor-pointer border border-slate-300 rounded-sm"
        @on-update-date="onUpdateActiveDate"
        @click="
          () => {
            caldendarModal = !caldendarModal;
          }
        "
      />
      <CalendarMonth
        v-if="caldendarModal"
        :activeDate="activeDate"
        @on-update-date="onUpdateActiveDate"
      />
    </div>
  </div>
</template>

<script>
import dayjs from "dayjs";

import CalendarMonth from "./components/CalendarMonth";

export default {
  name: "App",

  components: {
    CalendarMonth,
  },

  data() {
    return {
      caldendarModal: false,
      activeDate: ''
    }
  },
  computed: {
    today() {
      return dayjs().format("YYYY-MM-DD");
    }
  },
  methods: {
    onUpdateActiveDate(active) {
      this.activeDate = active
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.calendar-month-header {
  display: flex;
  justify-content: space-between;
  background-color: #fff;
  padding: 10px;
}

.calendar-input {
  width: 130px;
  padding-left: 23px;
  background: url("~@/assets/calendar.svg") no-repeat left;
  background-size: 18px;
}
</style>
