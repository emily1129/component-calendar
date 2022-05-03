<template>
  <div 
    :class="this.currentM === this.month.id ? 'text-white bg-red-500 font-medium' : ''"
    class="mx-auto p-3 w-14 h-14 text-center cursor-pointer rounded-full hover:bg-red-500 hover:text-white" 
    @click="updateActiveMonth">
    {{ this.month.name }}
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
      type: String
    }
  },
  methods: {
    updateActiveMonth() {
      this.$emit("update-active-month", this.month.id);
    }
  }
};
</script>
