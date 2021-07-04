<template>
  <div>
    <v-rows>
      <v-date-picker
        v-model="date"
        full-width
        color="primary"
        locale="ko-kr"
        @click:date="selectDate"
      />
    </v-rows>
    <v-rows>
      <v-calendar
        color="primary"
        locale="ko-kr"
        type="day"
        :value="selectedDate"
        :events="events"
        :event-ripple="false"
        @change="getEvents"
        @mousedown:time="startTime"
        @mousemove:time="mouseMove"
        @mouseup:time="endDrag"
        @mouseleave.native="cancelDrag"
      />
    </v-rows>
  </div>
</template>

<script>
export default {
  data: () => ({
    date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
    selectedDate: new Date(),
    value: '',
    events: [],
    dragStart: null,
    createEvent: null,
    createStart: null,
    extendOriginal: null
  }),
  methods: {
    startTime (tms) {
      const mouse = this.toTime(tms)

      this.createStart = this.roundTime(mouse)
      this.createEvent = {
        name: `Event #${this.events.length}`,
        color: '#2196F3',
        start: this.createStart,
        end: this.createStart,
        timed: true
      }

      this.events.push(this.createEvent)
    },
    mouseMove (tms) {
      const mouse = this.toTime(tms)

      if (this.createEvent && this.createStart !== null) {
        const mouseRounded = this.roundTime(mouse, false)
        const min = Math.min(mouseRounded, this.createStart)
        const max = Math.max(mouseRounded, this.createStart)

        // 기존 시간영역을 침범하는 이벤트 삭제 처리
        if (this.events
          .some(event => event !== this.createEvent && ((min >= event.start && min < event.end) || (max > event.start && max <= event.end)))) {
          this.events = this.events.filter(event => event !== this.createEvent)
          this.endDrag()
          return
        }

        this.createEvent.start = min
        this.createEvent.end = max
      }
    },
    endDrag () {
      // 시간 범위가 지정되지 않은 선택은 삭제 처리
      this.events = this.events.filter(event => event.start < event.end)

      console.log(this.events)

      this.dragTime = null
      this.createEvent = null
      this.createStart = null
      this.extendOriginal = null
    },
    cancelDrag () {
      if (this.createEvent) {
        if (this.extendOriginal) {
          this.createEvent.end = this.extendOriginal
        } else {
          const i = this.events.indexOf(this.createEvent)
          if (i !== -1) {
            this.events.splice(i, 1)
          }
        }
      }

      this.createEvent = null
      this.createStart = null
      this.dragTime = null
    },
    roundTime (time, down = true) {
      const roundTo = 30 // minutes
      const roundDownTime = roundTo * 60 * 1000

      return down
        ? time - time % roundDownTime
        : time + (roundDownTime - (time % roundDownTime))
    },
    toTime (tms) {
      return new Date(tms.year, tms.month - 1, tms.day, tms.hour, tms.minute).getTime()
    },
    getEvents ({ start, end }) {
      const events = []

      events.push({
        name: '테스트입니다',
        color: '#2196F3',
        start: new Date('2021-07-05T20:00:00').getTime(),
        end: new Date('2021-07-05T21:00:00').getTime(),
        timed: true
      })

      this.events = events
    },
    selectDate (date) {
      this.selectedDate = date
    }
  }
}
</script>
