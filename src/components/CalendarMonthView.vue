<template>
    <div>
        <div class="hearder-calendar">
            <span @click="selectPrevious" style="padding-right: 1rem; cursor: pointer;">preview</span>
            <span @click="selectCurrent">{{selectedDate.format("MMMM YYYY")}}</span>
            <span @click="selectNext" style="padding-left: 1rem; cursor: pointer;">next</span>
        </div>
        <div style="display:flex; flex: 50%;">
            <calendar-date-item
                v-for="day in dayFirstHalf"
                :key="day.date"
                :day="day"
                :is-current-day="day.isCurrentDay">
            </calendar-date-item>

            <calendar-date-item
                v-for="day in daySecondHalf"
                :key="day.date"
                :day="day"
                :is-current-day="day.isCurrentDay">
            </calendar-date-item>
        </div>
        
    </div>
</template>

<script>
import dayjs from "dayjs";
import CalendarDateItem from './CalendarDateItem.vue';
export default {
    name: "CalendarMonth",
    components: {
        CalendarDateItem
    },
    data() {
        return {
            selectedDate: dayjs(),
            today: dayjs().format("YYYY-MM-DD"),
        };
    },

    computed: {
        days() {
            return [
                ...this.currentMonthDays
            ];
        },

        daySecondHalf() {
            console.log('currentMonthDays', this.currentMonthDays);
            return 0;
            // if(this.currentMonthDays.length%2) {
                
            //     var arr = this.currentMonthDays.splice(this.currentMonthDays.length/2);
            //     return [
            //         ...arr
            //     ];
            // } else return [...this.currentMonthDays.splice(Math.round(this.currentMonthDays.length/2) + 1)];
        },

        dayFirstHalf() {
            return 0;
            // if(this.currentMonthDays.length%2) {
            //     this.currentMonthDays.splice(this.currentMonthDays.length/2);
            //     return [...this.currentMonthDays];
            // } else 
            // {
            //     this.currentMonthDays.splice(Math.round(this.currentMonthDays.length/2) + 1);
            //     return [...this.currentMonthDays];
            // }
        },

        month() {
            return Number(this.selectedDate.format("M"));
        },

        year() {
            return Number(this.selectedDate.format("YYYY"));
        },

        numberOfDaysInMonth() {
            return dayjs(`${this.year}-${this.month}-01`).daysInMonth();
        },

        currentMonthDays() {
            return [...Array(this.numberOfDaysInMonth)].map((day, index) => {
                return {
                    date: dayjs(`${this.year}-${this.month}-${index + 1}`).format(
                        "YYYY-MM-DD"
                    ),
                    dayOfMonth: index + 1,
                
                };
            });
        },

    // previousMonthDays() {
    //   const firstDayOfTheMonthWeekday = this.getWeekday(
    //     this.currentMonthDays[0].date
    //   );
    //   const previousMonth = dayjs(`${this.year}-${this.month}-01`).subtract(
    //     1,
    //     "month"
    //   );

    //   const previousMonthLastMondayDayOfMonth = dayjs(
    //     this.currentMonthDays[0].date
    //   )
    //     .subtract(firstDayOfTheMonthWeekday - 1, "day")
    //     .date();

    //   // Cover first day of the month being sunday (firstDayOfTheMonthWeekday === 0)
    //   const visibleNumberOfDaysFromPreviousMonth = firstDayOfTheMonthWeekday
    //     ? firstDayOfTheMonthWeekday - 1
    //     : 6;

    //   return [...Array(visibleNumberOfDaysFromPreviousMonth)].map(
    //     (day, index) => {
    //       return {
    //         date: dayjs(
    //           `${previousMonth.year()}-${previousMonth.month() +
    //             1}-${previousMonthLastMondayDayOfMonth + index}`
    //         ).format("YYYY-MM-DD"),
    //         dayOfMonth: previousMonthLastMondayDayOfMonth + index,
    //         isCurrentMonth: false
    //       };
    //     }
    //   );
    // },

    // nextMonthDays() {
    //   const lastDayOfTheMonthWeekday = this.getWeekday(
    //     `${this.year}-${this.month}-${this.currentMonthDays.length}`
    //   );

    //   const nextMonth = dayjs(`${this.year}-${this.month}-01`).add(1, "month");

    //   const visibleNumberOfDaysFromNextMonth = lastDayOfTheMonthWeekday
    //     ? 7 - lastDayOfTheMonthWeekday
    //     : lastDayOfTheMonthWeekday;

    //   return [...Array(visibleNumberOfDaysFromNextMonth)].map((day, index) => {
    //     return {
    //       date: dayjs(
    //         `${nextMonth.year()}-${nextMonth.month() + 1}-${index + 1}`
    //       ).format("YYYY-MM-DD"),
    //       dayOfMonth: index + 1,
    //       isCurrentMonth: false
    //     };
    //   });
    // }
    },
    methods: {
        selectPrevious() {
            console.log('preview');
            let newSelectedDate = dayjs(this.selectedDate).subtract(1, "month");
            console.log('newSelectedDate ', newSelectedDate);
            this.selectedDate = newSelectedDate;
            // this.$emit("dateSelected", newSelectedDate);
            // this.days = newSelectedDate;
        },

        selectCurrent() {
            console.log('current');
            let newSelectedDate = dayjs(this.today);
            console.log('newSelectedDate ', newSelectedDate);
            this.selectedDate = newSelectedDate;
            // this.$emit("dateSelected", newSelectedDate);
            // this.days = newSelectedDate;
        },

        selectNext() {
            console.log('next');
            let newSelectedDate = dayjs(this.selectedDate).add(1, "month");
            console.log('newSelectedDate ', newSelectedDate);
            this.selectedDate = newSelectedDate;
            // this.$emit("dateSelected", newSelectedDate);
            // this.days = newSelectedDate;
        }
    }
    
}
</script>