<template>
  <div class="p-6" @click="updateActiveMonth">
    <span
      :class="this.currentM === this.month.id ? 'text-white rounded-full bg-red-500 font-medium p-3' : ''"
      class="cursor-pointer p-3 rounded-full hover:bg-red-500 hover:text-white"
      >{{ this.month.name }}
    </span>
  </div>
</template>

<script>
export default {
  name: "CalendarMonthsView",
  props: {
    month: {
      require: true,
    },
    currentM: {
      type: String,
    },
  },
  methods: {
    updateActiveMonth() {
      this.$emit("update-active-month", this.month.id);
    },
  },
};
</script>
