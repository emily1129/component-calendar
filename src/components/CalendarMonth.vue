<template>
  <div>
    <div 
      class="calendar-month max-w-sm w-md-full border-2 p-4"
    >
      <div class="calendar-month-header">
        <CalendarDateSelector
          :current-date="today"
          :view-months="viewMonths"
          :currentM="currentM"
          :selected-date="selectedDate"
          @open-months="popupMonths"
          @dateSelected="selectDate"
        />
      </div>
      <CalendarWeekdays v-if="!viewMonths" />
      <div v-if="viewMonths" class="w-full grid grid-cols-3 min-h-full">
        <CalendarMonthsView
          v-for="month in months"
          :key="month.id"
          :month="month"
          :currentM="currentM"
          @update-active-month="updateMonth"
        />
      </div>
      <ol class="grid grid-cols-7" v-if="!viewMonths">
        <CalendarMonthDayItem
          v-for="day in days"
          :key="day.date"
          :day="day"
          :is-today="day.date === today"
          :active-date="activeDate"
          @on-update-date="updateActiveDate"
        />
      </ol>
    </div>
  </div>
</template>

<script>
import dayjs from "dayjs";
import weekday from "dayjs/plugin/weekday";
import weekOfYear from "dayjs/plugin/weekOfYear";
import CalendarDateSelector from "./CalendarDateSelector";
import CalendarMonthDayItem from "./CalendarMonthDayItem";
import CalendarWeekdays from "./CalendarWeekdays";
import CalendarMonthsView from "./CalendarMonthsView";

dayjs.extend(weekday);
dayjs.extend(weekOfYear);

export default {
  name: "CalendarMonth",

  components: {
    CalendarMonthDayItem,
    CalendarDateSelector,
    CalendarWeekdays,
    CalendarMonthsView,
  },
  
  data() {
    return {
      selectedDate: dayjs(),
      // activeDate: dayjs().format("YYYY-MM-DD"),
      activeDate: "",
      viewMonths: false,
      currentM: dayjs().format("MM"),
      stateOfMonth: null,
      // currentM: '',
      months: [
        {
          name: "Jan",
          id: "01",
        },
        {
          name: "Feb",
          id: "02",
        },
        {
          name: "Mar",
          id: "03",
        },
        {
          name: "Apr",
          id: "04",
        },
        {
          name: "May",
          id: "05",
        },
        {
          name: "Jun",
          id: "06",
        },
        {
          name: "Jul",
          id: "07",
        },
        {
          name: "Aug",
          id: "08",
        },
        {
          name: "Sep",
          id: "09",
        },
        {
          name: "Oct",
          id: "10",
        },
        {
          name: "Nov",
          id: "11",
        },
        {
          name: "Dec",
          id: "12",
        },
      ],
    };
  },
  computed: {
    days() {
      return [
        ...this.previousMonthDays,
        ...this.currentMonthDays,
        ...this.nextMonthDays,
      ];
    },

    today() {
      return dayjs().format("YYYY-MM-DD");
    },

    month() {
      return Number(this.selectedDate.format("M"));
    },

    month_date() {
      return Number(this.selectedDate.format("MMDD"));
    },

    year() {
      return Number(this.selectedDate.format("YYYY"));
    },

    numberOfDaysInMonth() {
      return dayjs(this.selectedDate).daysInMonth();
    },

    currentMonthDays() {
      return [...Array(this.numberOfDaysInMonth)].map((day, index) => {
        return {
          date: dayjs(`${this.year}-${this.month}-${index + 1}`).format(
            "YYYY-MM-DD"
          ),
          isCurrentMonth: true,
        };
      });
    },

    previousMonthDays() {
      const firstDayOfTheMonthWeekday = this.getWeekday(
        this.currentMonthDays[0].date // 2022-05-01
      );
      const previousMonth = dayjs(`${this.year}-${this.month}-01`).subtract(
        1,
        "month"
      );

      const visibleNumberOfDaysFromPreviousMonth = firstDayOfTheMonthWeekday
        ? firstDayOfTheMonthWeekday
        : 7;

      const previousMonthLastMondayDayOfMonth = dayjs(
        this.currentMonthDays[0].date
      )
        .subtract(visibleNumberOfDaysFromPreviousMonth, "day")
        .date();

      return [...Array(visibleNumberOfDaysFromPreviousMonth)].map(
        (day, index) => {
          return {
            date: dayjs(
              `${previousMonth.year()}-${previousMonth.month() + 1}-${
                previousMonthLastMondayDayOfMonth + index
              }`
            ).format("YYYY-MM-DD"),
            isCurrentMonth: false,
          };
        }
      );
    },

    nextMonthDays() {
      const nextMonth = dayjs(`${this.year}-${this.month}-01`).add(1, "month");

      const visibleNumberOfDaysFromNextMonth =
        42 - (this.currentMonthDays.length + this.previousMonthDays.length);

      return [...Array(visibleNumberOfDaysFromNextMonth)].map((day, index) => {
        return {
          date: dayjs(
            `${nextMonth.year()}-${nextMonth.month() + 1}-${index + 1}`
          ).format("YYYY-MM-DD"),
          isCurrentMonth: false,
        };
      });
    },
  },

  methods: {
    getWeekday(date) {
      return dayjs(date).weekday();
    },

    selectDate(newSelectedDate) {
      this.selectedDate = newSelectedDate;
    },

    updateActiveDate(label) {
      this.activeDate = label;
      this.$emit('on-update-date', this.activeDate)
    },

    popupMonths(trigger) {
      this.viewMonths = trigger;
    },

    updateMonth(updateMonth) {
      this.currentM = updateMonth;
    },
  },
};
</script>

<style scoped>
.calendar-month {
  position: relative;
  min-height: 300px;
  min-width: 300px;
}
</style>
