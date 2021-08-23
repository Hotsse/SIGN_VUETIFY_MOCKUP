<template>
  <v-row justify="center">
    <v-col cols="6">
      <v-card>
        <v-card-title>결재대기</v-card-title>
        <v-divider />
        <v-card-text>
          <v-tabs>
            <v-tab href="#sign">
              <v-badge
                content="2"
              >
                전자결재
              </v-badge>
            </v-tab>
            <v-tab href="#hr">
              인사
            </v-tab>
            <v-tab href="#contract">
              계약관리
            </v-tab>
            <v-tab-item id="sign" key="sign">
              <v-simple-table
                fixed-header
                height="500px"
              >
                <template #default>
                  <colgroup>
                    <col width="70%">
                    <col width="15%">
                    <col width="15%">
                  </colgroup>
                  <thead>
                    <tr>
                      <th class="text-center">제목</th>
                      <th class="text-center">신청자</th>
                      <th class="text-center">신청일</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr>
                      <td>
                        제목제목제목제목제목제목제목제목제목제목제목제목
                      </td>
                      <td class="text-center">
                        홍길동
                      </td>
                      <td class="text-center">
                        2021-08-23
                      </td>
                    </tr>
                    <tr>
                      <td>
                        제목제목제목제목제목제목제목제목제목제목제목제목
                      </td>
                      <td class="text-center">
                        홍길동
                      </td>
                      <td class="text-center">
                        2021-08-23
                      </td>
                    </tr>
                  </tbody>
                </template>
              </v-simple-table>
            </v-tab-item>
            <v-tab-item id="hr" key="hr" class="text-center" style="height:500px;">
              <h3 class="mt-8">결재 대기 항목이 없습니다.</h3>
            </v-tab-item>
            <v-tab-item id="contract" key="contract" class="text-center" style="height:500px;">
              <h3 class="mt-8">결재 대기 항목이 없습니다.</h3>
            </v-tab-item>
          </v-tabs>
        </v-card-text>
      </v-card>

      <v-card class="mt-3" height="260px">
        <v-card-title>법인카드 사용내역</v-card-title>
        <v-card-text>
          <v-row>
            <v-col cols="8">
              <h1>58,100원</h1>
            </v-col>
            <v-col cols="4">
              chart
            </v-col>
          </v-row>
        </v-card-text>
      </v-card>
    </v-col>
    <v-col cols="6">
      <v-card>
        <v-card-title>결재진행</v-card-title>
        <v-divider />
        <v-card-text>
          <v-tabs>
            <v-tab href="#sign">
              전자결재
            </v-tab>
            <v-tab href="#hr">
              인사
            </v-tab>
            <v-tab href="#contract">
              계약관리
            </v-tab>
            <v-tab-item id="sign" key="sign" style="height:800px;" align="center" justify="center">
              <v-simple-table
                fixed-header
                height="800px"
              >
                <template #default>
                  <colgroup>
                    <col width="66%">
                    <col width="6%">
                    <col width="14%">
                    <col width="14%">
                  </colgroup>
                  <tbody>
                    <tr>
                      <td class="pt-6 pb-6">
                        제목제목제목제목제목제목제목제목제목제목제목제목
                      </td>
                      <td class="text-center">
                        <v-chip
                          label
                          small
                        >
                          진행
                        </v-chip>
                      </td>
                      <td class="text-center">
                        홍길동
                      </td>
                      <td class="text-center">
                        2021-08-23
                      </td>
                    </tr>
                    <tr>
                      <td class="pt-6 pb-6">
                        제목제목제목제목제목제목제목제목제목제목제목제목
                      </td>
                      <td class="text-center">
                        <v-chip
                          label
                          small
                        >
                          진행
                        </v-chip>
                      </td>
                      <td class="text-center">
                        홍길동
                      </td>
                      <td class="text-center">
                        2021-08-23
                      </td>
                    </tr>
                  </tbody>
                </template>
              </v-simple-table>
            </v-tab-item>
            <v-tab-item id="hr" key="hr" class="text-center" style="height:800px;">
              <h3 class="mt-8">결재 진행 항목이 없습니다.</h3>
            </v-tab-item>
            <v-tab-item id="contract" key="contract" class="text-center" style="height:800px;">
              <h3 class="mt-8">결재 진행 항목이 없습니다.</h3>
            </v-tab-item>
          </v-tabs>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>
