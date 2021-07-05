<template>
  <div>
    <v-row>
      <v-col
        lg="4"
      >
        <v-row>
          <v-col>
            <DatePicker
              @select-date="selectDate"
            />
          </v-col>
        </v-row>
        <v-row>
          <v-col class="pt-1 pb-0">
            <v-select
              :items="buildings"
              item-text="text"
              item-value="value"
              label="회의실 선택"
              filled
            />
          </v-col>
        </v-row>
        <v-row>
          <v-col class="pt-0">
            <v-divider />
            <v-list>
              <v-list-item-group>
                <v-list-item
                  v-for="(room, i) in mtRooms"
                  :key="i"
                >
                  <v-list-item-content>
                    <v-list-item-title>- {{ i + 1 }}) {{ room.title }} ({{ room.count }}명)</v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
              </v-list-item-group>
            </v-list>
            <v-divider />
          </v-col>
        </v-row>
      </v-col>
      <v-col
        lg="8"
      >
        <v-row>
          <v-col>
            <v-text-field
              v-model="selectedDate"
              label="날짜"
              readonly
            />
            <v-select
              :items="[{text: '일반회의', value: '000001'}, {text: '정기회의', value: '000002'}]"
              item-text="text"
              item-value="value"
              label="구분"
            />
            <v-text-field
              v-model="selectedTime"
              label="시간"
              readonly
            />
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-calendar
              color="primary"
              locale="ko-kr"
              type="day"
              first-time="07:00"
              interval-count="17"
              :value="selectedDate"
              :events="events"
              @change="getEvents"
              @mousedown:time="startTime"
              @mousemove:time="mouseMove"
              @mouseup:time="endDrag"
              @mouseleave.native="cancelDrag"
            />
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import DatePicker from '@/components/util/time/DatePicker.vue'
export default {
  components: {
    DatePicker
  },
  data: () => ({
    buildings: [
      { text: '넥슨 10F', value: '123456' },
      { text: '넥슨 9F', value: '123455' }
    ],
    mtRooms: [
      { title: '넥슨 10F - A1', count: 6 },
      { title: '넥슨 10F - A2', count: 8 },
      { title: '넥슨 10F - A3', count: 8 }
    ],
    selectedDate: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
    selectedStartTime: null,
    selectedEndTime: null,
    disabledDates: { weekdays: [1, 7] },
    value: '',
    events: [],
    dragStart: null,
    createEvent: null,
    createStart: null,
    extendOriginal: null
  }),
  computed: {
    selectedTime () {
      return `${this.selectedStartTime} ~ ${this.selectedEndTime}`
    }
  },
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
        this.selectedStartTime = (new Date(new Date(min) - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(11, 5)
        this.selectedEndTime = (new Date(new Date(max) - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(11, 5)
      }
    },
    endDrag () {
      // 시간 범위가 지정되지 않은 선택은 삭제 처리
      this.events = this.events.filter(event => event.start < event.end)

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
    },
    allowedOnlyWeekday (val) {
      // 평일만 선택 활성화
      return [1, 2, 3, 4, 5].includes(new Date(Date.parse(val)).getDay())
    }
  }
}
</script>
