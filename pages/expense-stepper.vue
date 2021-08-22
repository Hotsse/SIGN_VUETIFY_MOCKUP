<template>
  <v-stepper
    v-model="step"
  >
    <v-stepper-header>
      <v-stepper-step
        :complete="step > 1"
        step="1"
      >
        예산정보 선택
      </v-stepper-step>

      <v-divider />

      <v-stepper-step
        :complete="step > 2"
        step="2"
      >
        법인카드 사용내역 선택
      </v-stepper-step>

      <v-divider />

      <v-stepper-step
        :complete="step > 3"
        step="3"
      >
        상신
      </v-stepper-step>
    </v-stepper-header>
    <v-stepper-items>
      <v-stepper-content step="1">
        <BudStepper
          @select-bud-info="selectBudInfo"
        />
      </v-stepper-content>
      <v-stepper-content step="2">
        <CmsCardSelects
          @select-cms-card="selectCmsCard"
        />
        <CmsDataTables
          ref="cmsDatas"
        />
        <v-btn
          block
          color="primary"
          @click="selectCmsDatas()"
        >
          선택
        </v-btn>
      </v-stepper-content>
      <v-stepper-content step="3">
        <div>
        </div>
        <div class="text-center">
          <p>bud : {{ bud != null ? bud.title : '' }}</p>
          <p>cc : {{ cc != null ? cc.title : '' }}</p>
          <p>acct : {{ acct != null ? acct.title : '' }}</p>
          <p>cmsCard : {{ cmsCard }}</p>
          <p>cmsDatas : {{ cmsDatas }}</p>
          <ApprGrpLines
            :appr-grp-lines="apprGrpLines"
            :appr-to-ccs="apprToCcs"
          />
        </div>
      </v-stepper-content>
    </v-stepper-items>
  </v-stepper>
</template>

<script>
import CmsCardSelects from '@/components/business/budcost/CmsCardSelects.vue'
import CmsDataTables from '@/components/business/budcost/CmsDataTables.vue'
import BudStepper from '@/components/business/budcost/BudStepper.vue'
import ApprGrpLines from '@/components/business/appr/ApprGrpLines.vue'

export default {
  components: {
    CmsCardSelects,
    CmsDataTables,
    BudStepper,
    ApprGrpLines
  },
  data: () => ({
    step: 1,
    bud: null,
    cc: null,
    acct: null,
    cmsCard: null,
    cmsDatas: null,
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
    selectBudInfo (bud, cc, acct) {
      console.log(bud)
      console.log(cc)
      console.log(acct)

      this.bud = bud
      this.cc = cc
      this.acct = acct

      this.step = 2
    },
    selectCmsCard (card) {
      console.log(card)

      this.cmsCard = card
      this.$refs.cmsDatas.setCmsCard(card)
    },
    selectCmsDatas () {
      const datas = this.$refs.cmsDatas.selectCmsDatas()
      if (datas != null) {
        console.log(datas)
        this.cmsDatas = datas
        this.step = 3
      }
    }
  }
}
</script>
