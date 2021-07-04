<template>
  <v-tabs>
    <v-tab href="#operBud">
      운영비
    </v-tab>
    <v-tab href="#actBud">
      집행예산
    </v-tab>
    <v-tab-item id="operBud" key="operBud">
      <v-list>
        <v-list-item-group>
          <v-list-item
            v-for="(operBud, i) in operBuds"
            :key="i"
            @click="selectOperBud(operBud)"
          >
            <v-list-item-content>
              <v-list-item-title>{{ operBud.title }}</v-list-item-title>
              <v-list-item-subtitle>{{ operBud.amt }}원</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-tab-item>
    <v-tab-item id="actBud" key="actBud">
      <v-list>
        <v-list-item-group>
          <v-list-item
            v-for="(actBud, i) in actBuds"
            :key="i"
            @click="selectActBud(actBud)"
          >
            <v-list-item-content>
              <v-list-item-title>{{ actBud.title }}</v-list-item-title>
              <v-list-item-subtitle>{{ actBud.amt }}원</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-tab-item>
  </v-tabs>
</template>

<script>
export default {
  data: () => ({
    operBuds: [
      { title: '재무그룹웨어팀 운영비', operBudNo: '111111', amt: '100000' }
    ],
    actBuds: [
      { title: '[Tax팀] 이현 세무자문 용역 지급의 건', actBudNo: '222222', amt: '0' },
      { title: '넥슨공통-외근교통비', actBudNo: '333333', amt: '******' }
    ]
  }),
  methods: {
    selectOperBud (operBud) {
      this.$emit('select-oper-bud', operBud)
    },
    selectActBud (actBud) {
      this.$emit('select-act-bud', actBud)
    }
  }
}
</script>
