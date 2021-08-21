<template>
  <v-row justify="center" align="center">
    <v-col cols="6">
      <v-tabs>
        <v-tab href="#sign">
          전자결재
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
                <col width="85%">
                <col width="15%">
              </colgroup>
              <tbody>
                <tr>
                  <td>
                    제목제목제목제목제목제목제목제목제목제목제목제목
                  </td>
                  <td class="text-center">
                    홍길동
                  </td>
                </tr>
                <tr>
                  <td>
                    제목제목제목제목제목제목제목제목제목제목제목제목
                  </td>
                  <td class="text-center">
                    홍길동
                  </td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>
        </v-tab-item>
        <v-tab-item id="contract" key="contract" class="text-center" style="height:500px;">
          <h3 class="mt-8">데이터가 존재하지 않습니다.</h3>
        </v-tab-item>
      </v-tabs>
    </v-col>
    <v-col cols="6">
      <v-tabs>
        <v-tab href="#progress">
          결재진행함
        </v-tab>
        <v-tab href="#pending">
          결재대기함
        </v-tab>
        <v-tab-item id="progress" key="progress" class="text-center" style="height:500px;">
          <h3 class="mt-8">데이터가 존재하지 않습니다.</h3>
        </v-tab-item>
        <v-tab-item id="pending" key="pending" class="text-center" style="height:500px;">
          <h3 class="mt-8">데이터가 존재하지 않습니다.</h3>
        </v-tab-item>
      </v-tabs>
    </v-col>
  </v-row>
</template>
