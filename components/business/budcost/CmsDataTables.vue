<template>
  <v-card>
    <v-card-title>법인카드 사용내역 선택</v-card-title>
    <v-card-text
      align="center"
      justify="center"
    >
      <div
        v-if="cmsDatas == null"
        class="text-center"
        style="height:500px;line-height:500px;"
      >
        <span style="vertical-align: middle;">법인카드를 선택해 주세요</span>
      </div>
      <div
        v-else-if="cmsDatas.length <= 0"
        class="text-center"
        style="height:500px;line-height:500px;"
      >
        <span style="vertical-align: middle;">사용내역이 존재하지 않습니다</span>
      </div>
      <v-simple-table
        v-else
        fixed-header
        height="500px"
      >
        <template #default>
          <colgroup>
            <col width="5%">
            <col width="15%">
            <col width="15%">
            <col width="10%">
            <col width="10%">
            <col width="25%">
            <col width="10%">
            <col width="10%">
          </colgroup>
          <thead>
            <tr>
              <th class="text-center">
                &nbsp;
              </th>
              <th class="text-center">
                승인처
              </th>
              <th class="text-center">
                승인일시
              </th>
              <th class="text-center">
                공급가액
              </th>
              <th class="text-center">
                세액
              </th>
              <th class="text-center">
                사용내역
              </th>
              <th class="text-center">
                접대비 명세서
              </th>
              <th class="text-center">
                청탁금지 명세서
              </th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="(cms, i) in cmsDatas"
              :key="i"
            >
              <td class="text-center">
                <v-checkbox
                  v-model="cms.selected"
                />
              </td>
              <td>
                {{ cms.title }}
              </td>
              <td class="text-center">
                {{ cms.apprDtt }}
              </td>
              <td class="text-center">
                {{ cms.amt }}원
              </td>
              <td class="text-center">
                {{ cms.tax }}원
              </td>
              <td class="text-center">
                <v-textarea
                  v-model="cms.content"
                  rows="2"
                  hint="사용내역 입력"
                />
              </td>
              <td class="text-center">
                <v-btn
                  small
                  color="primary"
                  :disabled="cms.amt > REP_AMT"
                >
                  첨부
                </v-btn>
              </td>
              <td class="text-center">
                <v-btn
                  small
                  color="primary"
                >
                  첨부
                </v-btn>
              </td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  data: () => ({
    cmsCard: null,
    cmsDatas: null,
    REP_AMT: 100000
  }),
  methods: {
    setCmsCard (card) {
      this.cmsCard = card
      this.cmsDatas = [
        { cmsNo: '12345678', title: '풍무양꼬치 구로디지털단지점', apprDtt: '2021-07-04 19:00:00', amt: '53000', tax: '5300' },
        { cmsNo: '23456789', title: '최우영 스시', apprDtt: '2021-07-03 19:00:00', amt: '214000', tax: '21400' },
        { cmsNo: '34567890', title: '새마을식당 판교점', apprDtt: '2021-07-02 19:00:00', amt: '78500', tax: '7850' },
        { cmsNo: '45678901', title: '버거킹 서현역점', apprDtt: '2021-07-01 19:00:00', amt: '53000', tax: '5300' },
        { cmsNo: '56789012', title: '은행골 서현점', apprDtt: '2021-06-30 19:00:00', amt: '214000', tax: '21400' },
        { cmsNo: '67890123', title: '스시하루 판교점', apprDtt: '2021-06-29 19:00:00', amt: '78500', tax: '7850' }
      ]
    },
    selectCmsDatas () {
      if (this.cmsCard == null || this.cmsDatas == null) {
        this.$nuxt.$emit('onSnackBar', '법인카드를 선택해 주세요', 2000)
        return null
      }
      const selectedDatas = this.cmsDatas.filter(cmsData => cmsData.selected === true)

      if (selectedDatas.length <= 0) {
        this.$nuxt.$emit('onSnackBar', '법인카드 사용내역을 선택해 주세요', 2000)
        return null
      } else if (selectedDatas.some(data => !data.content)) {
        this.$nuxt.$emit('onSnackBar', '선택한 항목에 대한 사용내역을 입력해 주세요', 2000)
        return null
      }
      return selectedDatas
    }
  }
}
</script>
