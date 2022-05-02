<template>
  <div class="flex justify-between w-screen text-gray-800 font-bold">
    <span @click="selectPrevious">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-5 w-5 mt-1"
        viewBox="0 0 20 20"
        fill="currentColor"
      >
        <path
          fill-rule="evenodd"
          d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z"
          clip-rule="evenodd"
        />
      </svg>
    </span>
    <div 
      class="w-1/2 p-1 cursor-pointer"
      @click="openMonths"  
    >
      {{ selectedMonth }}
    </div>
    <span @click="selectNext">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-5 w-5 mt-1"
        viewBox="0 0 20 20"
        fill="currentColor"
      >
        <path
          fill-rule="evenodd"
          d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
          clip-rule="evenodd"
        />
      </svg>
    </span>
  </div>
</template>

<script>
import dayjs from "dayjs";

export default {
  name: "CalendarModeSelector",

  props: {
    currentDate: {
      type: String,
      required: true,
    },

    selectedDate: {
      type: Object,
      required: true,
    },
    
    viewMonths: {
      type: Boolean,
      require: true
    },

    currentM: {
      type: String,
      require: true
    }
  },

  computed: {
    selectedMonth() {
      return this.selectedDate.format("MMMM YYYY");
    }
  },
  methods: {
    selectPrevious() {
      let newSelectedDate = dayjs(this.selectedDate).subtract(1, "month");
      this.$emit("dateSelected", newSelectedDate);
    },

    selectCurrent() {
      let newSelectedDate = dayjs(this.currentDate);
      this.$emit("dateSelected", newSelectedDate);
    },

    selectNext() {
      let newSelectedDate = dayjs(this.selectedDate).add(1, "month");
      this.$emit("dateSelected", newSelectedDate);
    },

    openMonths() {
      this.$emit("open-months", !this.viewMonths)
    }
  },
};
</script>
