<template>
  <v-date-picker
    v-model="selectedDate"
    :allowed-dates="allowedOnlyWeekday"
    full-width
    color="primary"
    locale="ko-kr"
    @click:date="selectDate"
  />
</template>

<script>
export default {
  data: () => ({
    selectedDate: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10)
  }),
  methods: {
    selectDate (date) {
      this.$emit('select-date', date)
    },
    allowedOnlyWeekday (val) {
      // 평일만 선택 활성화
      return [1, 2, 3, 4, 5].includes(new Date(Date.parse(val)).getDay())
    }
  }
}
</script>
