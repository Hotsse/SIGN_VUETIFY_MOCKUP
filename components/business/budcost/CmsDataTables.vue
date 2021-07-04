<template>
  <v-card>
    <v-card-title>법인카드 사용내역 선택</v-card-title>
    <v-card-text>
      <v-simple-table
        fixed-header
        height="300px"
      >
        <template #default>
          <colgroup>
            <col width="5%"></col>
            <col width="15%"></col>
            <col width="15%"></col>
            <col width="10%"></col>
            <col width="10%"></col>
            <col width="25%"></col>
            <col width="10%"></col>
            <col width="10%"></col>
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
                뭐드라 명세서
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
                  v-model="selectedCmsNos"
                  :value="cms.cmsNo"
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
                  rows="2"
                  hint="사용내역 입력"
                />
              </td>
              <td class="text-center">
                <v-btn
                  small
                  color="primary"
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
    selectedCmsNos: [],
    cmsDatas: [
      { cmsNo: '12345678', title: '풍무양꼬치 구로디지털단지점', apprDtt: '2021-07-04 19:00:00', amt: '53000', tax: '5300' },
      { cmsNo: '23456789', title: '최우영 스시', apprDtt: '2021-07-03 19:00:00', amt: '214000', tax: '21400' },
      { cmsNo: '34567890', title: '새마을식당 판교점', apprDtt: '2021-07-02 19:00:00', amt: '78500', tax: '7850' }
    ]
  }),
  watch: {
    selectedCmsNos (newValue) {
      this.$emit('select-cms-datas', newValue)
    }
  }
}
</script>
