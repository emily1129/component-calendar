<template>
  <div class="flex justify-between w-screen text-gray-800 font-bold">
    <template v-if="!viewMonths">
      <span @click="selectPrevious">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5 mt-1 cursor-pointer"
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
        v-if="!viewMonths"
        class="w-1/2 p-1 cursor-pointer bg-gray-100"
        @click="openMonths"
      >
        {{ selectedMonth[0] }} {{ selectedMonth[1] }}
      </div>
      <span @click="selectNext">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5 mt-1 cursor-pointer"
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
    </template>
     <template v-if="viewMonths">
      <span @click="selectPrevious">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5 mt-1 cursor-pointer"
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
      v-if="viewMonths"
      class="w-1/2 p-1 cursor-pointer"
      @click="openMonths"  
    >
      {{ selectedMonth[1] }}
    </div>
      <span @click="selectNext">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5 mt-1 cursor-pointer"
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
    </template>
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
      require: true,
    },

    currentM: {
      type: String,
      require: true,
    },
  },

  computed: {
    selectedMonth() {
      let selectedDate = [];
      selectedDate.push(
        this.selectedDate.format("MMMM"),
        this.selectedDate.format("YYYY")
      );
      return selectedDate;
    },
  },
  methods: {
    selectPrevious() {
      let newSelectedDate = dayjs(this.selectedDate).subtract(1, "month");
      this.$emit("dateSelected", newSelectedDate);
    },

    selectPreviousYear() {
      let newSelectedDate = dayjs(this.selectedDate).subtract(1, "year");
      this.$emit("update-active-month", newSelectedDate);
    },

    selectCurrent() {
      let newSelectedDate = dayjs(this.currentDate);
      this.$emit("dateSelected", newSelectedDate);
    },

    selectNext() {
      let newSelectedDate = dayjs(this.selectedDate).add(1, "month");
      this.$emit("dateSelected", newSelectedDate);
    },

    selectNextYear() {
      let newSelectedDate = dayjs(this.selectedDate).add(1, "year");
      this.$emit("update-active-month", newSelectedDate);
    },
  
    openMonths() {
      this.$emit("open-months", !this.viewMonths);
    },
  },
};
</script>
