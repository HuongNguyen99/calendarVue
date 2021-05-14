<template>
    <div class="dayItem">
        <div class="weekday">{{ label }}</div>
        <div class="day">{{ labelDay }}</div>
    </div>
</template>

<script>
import dayjs from 'dayjs';

const weekDay = {
    0: 'Sun',
    1: 'Mon',
    2: 'Tue',
    3: 'Wed',
    4: 'Thu',
    5: 'Fri',
    6: 'Sat'
};

export default {
    name: 'CalendarDateItem',
    props: {

        day: {
            type: Object,
            require: true
        },

        isCurrentDay: {
            type: Boolean,
            default: false
        }
    },
    computed: {
        labelDay() {
            return dayjs(this.day.date).format("DD / MM / YYYY");
        },
        label() {
            const indexDay = dayjs(this.day.date).day();
            return weekDay[indexDay];
        }
    }

}
</script>

<style scoped>
.dayItem {
    display: flex;
    width: 100%;
}
.weekday {
    width: fit-content;
    flex: 10%;
    border: 1px solid #f1f1f1;
    padding: 0.5rem 1rem;
}
.day {
    flex: 90%;
    border: 1px solid #f1f1f1;
    padding: 0.5rem 1rem;
}
</style>