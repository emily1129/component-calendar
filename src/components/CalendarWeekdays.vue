<template>
  <ol class="m-1 grid grid-cols-7 font-bold">
    <li v-for="weekday in weekdays" :key="weekday">{{ weekday }}</li>
  </ol>
</template>

<script>

export default {
  name: "CalendarWeekdays",
  data() {
    return {
      weekdays: ["Su", "Mo", "Tu", "We", "Th", "Fr", "Sa"]
    }
  }
};
</script>
