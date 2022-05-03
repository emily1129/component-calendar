<template>
  <li
    class="calendar-day relative p-2 font-medium"
    :class="{
      'text-gray-300': !day.isCurrentMonth,
      'text-red-600': isToday,
    }"
    @click="updateActiveDate"
  >
    <span 
      class="absolute flex justify-center items-center w-4 h-4 p-4 cursor-pointer hover:text-red-700 hover:bg-red-200 hover:rounded-full"
      :class="activeDate === this.label ? 'p-4 text-white bg-red-500 rounded-full' : '' "
    >{{ this.output }}</span>
  </li>
</template>

<script>
import dayjs from "dayjs";

export default {
  name: "CalendarMonthDayItem",

  data(){
    return{
      output: dayjs(this.day.date).format("D"),
      label: dayjs(this.day.date).format("YYYY-MM-DD"),
    }
  },
  props: {
    day: {
      type: Object,
      required: true
    },

    isCurrentMonth: {
      type: Boolean,
      default: false
    },

    isToday: {
      type: Boolean,
      default: false
    },

    activeDate: {
      default: false
    }
  },

  methods: {
    updateActiveDate() {
      this.$emit('on-update-date', this.label)
    }
  }

};
</script>

<style scoped>
.calendar-day {
  min-height: 45px;
}
</style>
