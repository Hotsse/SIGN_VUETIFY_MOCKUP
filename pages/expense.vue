<template>
  <div>
    <CmsCardSelects
      @select-cms-card="selectCmsCard"
    />
    <CmsDataTables
      @select-cms-datas="selectCmsDatas"
    />
    <BudStepper
      @select-bud-info="selectBudInfo"
    />
  </div>
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
    }
  }
}
</script>
