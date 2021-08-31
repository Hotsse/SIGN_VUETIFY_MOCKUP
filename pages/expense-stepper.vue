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
          ref="budStepper"
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
        <div class="mt-8">
          <StepperNav
            @prev-callback="step=1;$refs.budStepper.initialize();"
            @next-callback="selectCmsDatas()"
          />
        </div>
      </v-stepper-content>
      <v-stepper-content step="3">
        <div>
          <ApprGrpLines
            class="text-center"
            :appr-grp-lines="apprGrpLines"
            :appr-to-ccs="apprToCcs"
          />
        </div>
        <div class="mt-8">
          <v-simple-table>
            <template #default>
              <tbody>
                <tr>
                  <td>예산</td>
                  <td class="text-right pr-4">
                    {{ bud != null ? bud.title : '' }}
                  </td>
                </tr>
                <tr>
                  <td>프로젝트</td>
                  <td class="text-right pr-4">
                    {{ cc != null ? cc.title : '' }}
                  </td>
                </tr>
                <tr>
                  <td>회계계정</td>
                  <td class="text-right pr-4">
                    {{ acct != null ? acct.title : '' }}
                  </td>
                </tr>
                <tr>
                  <td>법인카드</td>
                  <td class="text-right pr-4">
                    {{ cmsCard }}
                  </td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>
          <v-expansion-panels>
            <v-expansion-panel
              v-for="(cmsData,i) in cmsDatas"
              :key="i"
            >
              <v-expansion-panel-header>
                {{ cmsData.title }}
                <span class="text-right mr-3">
                  {{ cmsData.amt }} 원
                </span>
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                <v-simple-table>
                  <template #default>
                    <tbody>
                      <tr>
                        <td>사용내역</td>
                        <td class="text-right mr-3">
                          {{ cmsData.content }}
                        </td>
                      </tr>
                      <tr>
                        <td>승인일</td>
                        <td class="text-right mr-3">
                          {{ cmsData.apprDtt }}
                        </td>
                      </tr>
                      <tr>
                        <td>공급가액</td>
                        <td class="text-right mr-3">
                          {{ cmsData.amt }}
                        </td>
                      </tr>
                      <tr>
                        <td>세액</td>
                        <td class="text-right mr-3">
                          {{ cmsData.tax }}
                        </td>
                      </tr>
                    </tbody>
                  </template>
                </v-simple-table>
              </v-expansion-panel-content>
            </v-expansion-panel>
          </v-expansion-panels>
        </div>
        <div class="mt-8">
          <StepperNav
            prev-name="이전"
            next-name="상신"
            @prev-callback="step=2"
            @next-callback=";"
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
import StepperNav from '@/components/business/common/StepperNav.vue'
import ApprGrpLines from '@/components/business/appr/ApprGrpLines.vue'

export default {
  components: {
    CmsCardSelects,
    CmsDataTables,
    BudStepper,
    StepperNav,
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
