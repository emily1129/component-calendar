<template>
  <div class="p-6" @click="updateActiveMonth">
    <span
      :class="this.currentM === this.month.id ? 'text-white rounded-full bg-red-500 font-medium p-3' : ''"
      class="month-name rounded-full hover:bg-red-500 hover:text-white"
      >{{ this.month.name }}
    </span>
  </div>
</template>

<script>
export default {
  name: "CalendarYearsView",
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
<style scoped>
.month-name {
  padding-top: 16px;
  padding-bottom: 16px;
}
</style>