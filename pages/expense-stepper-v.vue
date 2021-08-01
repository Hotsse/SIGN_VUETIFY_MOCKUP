<template>
  <v-stepper
    v-model="step"
    vertical
  >
    <v-stepper-step
      :complete="step > 1"
      step="1"
    >
      법인카드 선택
    </v-stepper-step>
    <v-stepper-content step="1">
      <CmsCardSelects
        @select-cms-card="selectCmsCard"
      />
      <v-btn
        block
        color="primary"
        @click="step = 2"
      >
        선택
      </v-btn>
    </v-stepper-content>

    <v-stepper-step
      :complete="step > 2"
      step="2"
    >
      법인카드 사용내역 선택
    </v-stepper-step>
    <v-stepper-content step="2">
      <CmsDataTables
        @select-cms-datas="selectCmsDatas"
      />
      <v-btn
        block
        color="primary"
        @click="step = 3"
      >
        선택
      </v-btn>
    </v-stepper-content>

    <v-stepper-step
      :complete="step > 3"
      step="3"
    >
      예산정보 선택
    </v-stepper-step>
    <v-stepper-content step="3">
      <BudStepper
        @select-bud-info="selectBudInfo"
      />
    </v-stepper-content>
  </v-stepper>
</template>

<script>
import CmsCardSelects from '@/components/business/budcost/CmsCardSelects.vue'
import CmsDataTables from '@/components/business/budcost/CmsDataTables.vue'
import BudStepper from '@/components/business/budcost/BudStepper.vue'
export default {
  components: {
    CmsCardSelects,
    CmsDataTables,
    BudStepper
  },
  data: () => ({
    step: 1,
    bud: null,
    cc: null,
    acct: null,
    cmsCard: null,
    cmsDatas: null
  }),
  methods: {
    selectCmsCard (card) {
      console.log(card)

      this.cmsCard = card
    },
    selectCmsDatas (cmsDatas) {
      console.log(cmsDatas)

      this.cmsDatas = cmsDatas
    },
    selectBudInfo (bud, cc, acct) {
      console.log(bud)
      console.log(cc)
      console.log(acct)

      this.bud = bud
      this.cc = cc
      this.acct = acct

      this.step = 4
    }
  }
}
</script>
