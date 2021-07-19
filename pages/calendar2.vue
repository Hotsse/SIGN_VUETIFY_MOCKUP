<template>
  <div>
    <div>
      <h3 class="mb-1">
        결재선
      </h3>
      <v-divider />
      <div class="text-center mt-3">
        <ApprGrpLines
          :appr-grp-lines="apprGrpLines"
          :appr-to-ccs="apprToCcs"
        />
      </div>
    </div>
    <div>
      <v-btn
        fab
        text
        small
        color="grey darken-2"
        @click="prev"
      >
        <v-icon small>
          mdi-chevron-left
        </v-icon>
      </v-btn>
      <v-btn
        fab
        text
        small
        color="grey darken-2"
        @click="next"
      >
        <v-icon small>
          mdi-chevron-right
        </v-icon>
      </v-btn>
      <v-calendar
        ref="calendar"
        v-model="value"
        color="primary"
        locale="ko-kr"
        type="week"
        :value="selectedDate"
        :events="events"
        :weekdays="weekday"
        @change="getEvents"
        @mousedown:time="startTime"
        @mousemove:time="mouseMove"
        @mouseup:time="endDrag"
        @mouseleave.native="cancelDrag"
      />
    </div>
  </div>
</template>

<script>
import ApprGrpLines from '@/components/business/appr/ApprGrpLines.vue'
export default {
  components: {
    ApprGrpLines
  },
  data: () => ({
    weekday: [1, 2, 3, 4, 5],
    value: '',
    events: [],
    dragStart: null,
    createEvent: null,
    createStart: null,
    extendOriginal: null,
    selectedDate: null,
    apprToCcs: {
      tos: [
        {
          empDeptYn: 'D',
          cmpCd: 'NX',
          empDeptNo: 51212,
          empDeptNm: '재무그룹웨어팀'
        }
      ],
      ccs: [
        {
          empDeptYn: 'E',
          cmpCd: 'NX',
          empDeptNo: 24687,
          empDeptNm: '윤호세'
        }
      ],
      bccs: []
    },
    apprGrpLines: [
      {
        grpNm: null,
        grpStsNm: '상신',
        apprLines: [
          {
            empNo: 24687,
            empNm: '윤호세',
            dutyNm: '팀원',
            deptNm: '재무그룹웨어팀'
          }
        ]
      },
      {
        grpNm: null,
        grpStsNm: '결재',
        apprLines: [
          {
            empNo: 19063,
            empNm: '박민성',
            dutyNm: '팀원',
            deptNm: '재무그룹웨어팀'
          },
          {
            empNo: 23237,
            empNm: '최민호3',
            dutyNm: '팀원',
            deptNm: '재무그룹웨어팀'
          }
        ]
      },
      {
        grpNm: null,
        grpStsNm: '결재',
        apprLines: [
          {
            empNo: 14838,
            empNm: '최다희',
            dutyNm: '팀장',
            deptNm: '재무그룹웨어팀'
          }
        ]
      },
      {
        grpNm: '경비/매입 담당그룹',
        grpStsNm: '담당',
        apprLines: [
          {
            empNo: 11111,
            empNm: '나회계',
            dutyNm: '팀원',
            deptNm: '회계2팀'
          },
          {
            empNo: 22222,
            empNm: '박회계',
            dutyNm: '팀원',
            deptNm: '회계2팀'
          },
          {
            empNo: 33333,
            empNm: '정회계',
            dutyNm: '팀원',
            deptNm: '회계2팀'
          }
        ]
      }
    ]
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
    },
    prev () {
      this.$refs.calendar.prev()
    },
    next () {
      this.$refs.calendar.next()
    }
  }
}
</script>
