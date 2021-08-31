<template>
  <v-card>
    <v-card-title>예산정보 선택</v-card-title>
    <v-card-text>
      <v-stepper
        v-model="step"
        vertical
      >
        <v-stepper-step
          :complete="step > 1"
          step="1"
        >
          <span v-if="bud == null">예산 선택</span>
          <span v-else>{{ bud.title }}</span>
        </v-stepper-step>

        <v-stepper-content step="1">
          <BudLists
            @select-oper-bud="selectOperBud"
            @select-act-bud="selectActBud"
          />
        </v-stepper-content>

        <v-stepper-step
          :complete="step > 2"
          step="2"
        >
          <span v-if="cc == null">프로젝트 선택</span>
          <span v-else>{{ cc.title }}</span>
        </v-stepper-step>

        <v-stepper-content step="2">
          <CcLists
            @select-cc="selectCc"
          />
        </v-stepper-content>

        <v-stepper-step
          :complete="step > 3"
          step="3"
        >
          <span v-if="acct == null">계정과목 선택</span>
          <span v-else>{{ acct.title }}</span>
        </v-stepper-step>

        <v-stepper-content step="3">
          <AcctLists
            @select-acct="selectAcct"
          />
        </v-stepper-content>
      </v-stepper>
    </v-card-text>
  </v-card>
</template>

<script>
import BudLists from '@/components/business/budcost/BudLists.vue'
import CcLists from '@/components/business/budcost/CcLists.vue'
import AcctLists from '@/components/business/budcost/AcctLists.vue'
export default {
  components: {
    BudLists,
    CcLists,
    AcctLists
  },
  data: () => ({
    bud: null,
    cc: null,
    acct: null,
    step: 1
  }),
  methods: {
    selectOperBud (operBud) {
      this.bud = operBud
      this.step = 2
    },
    selectActBud (actBud) {
      this.bud = actBud
      this.step = 2
    },
    selectCc (cc) {
      this.cc = cc
      this.step = 3
    },
    selectAcct (acct) {
      this.acct = acct
      this.step = 4
      this.$emit('select-bud-info', this.bud, this.cc, this.acct)
    },
    initialize () {
      this.bud = null
      this.cc = null
      this.acct = null
      this.step = 1
    }
  }
}
</script>
