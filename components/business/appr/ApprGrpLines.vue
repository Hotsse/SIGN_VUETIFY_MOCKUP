<template>
  <div>
    <v-menu
      v-for="(apprGrpLine, grpIdx) in apprGrpLines"
      :key="grpIdx"
      open-on-hover
      bottom
      offset-y
    >
      <template #activator="{ on, attrs }">
        <v-card
          outlined
          class="d-inline-block mr-5"
          min-width="150px"
          v-bind="attrs"
          v-on="on"
        >
          <v-card-subtitle class="accent text-center pa-1">
            {{ apprGrpLine.grpStsNm }}
          </v-card-subtitle>
          <v-card-text class="text-center mt-3">
            <div>
              <span v-if="apprGrpLine.grpNm !== null">{{ apprGrpLine.grpNm }}</span>
              <span v-else-if="apprGrpLine.apprLines.length > 1">{{ apprGrpLine.apprLines[0].empNm }} 외 {{ apprGrpLine.apprLines.length - 1 }}명</span>
              <span v-else>{{ apprGrpLine.apprLines[0].empNm }} {{ apprGrpLine.apprLines[0].dutyNm }}</span>
            </div>
            <div>
              2021-07-16
            </div>
          </v-card-text>
        </v-card>
      </template>
      <v-list three-line>
        <v-subheader>
          구성원
        </v-subheader>
        <template v-for="(apprLine, idx) in apprGrpLine.apprLines">
          <v-divider v-if="idx > 0" :key="'divider_' + grpIdx + '_' + idx" />
          <v-list-item
            :key="'list_' + grpIdx + '_' + idx"
          >
            <v-list-item-avatar color="primary">
              <!--
              <v-img v-if="appr" :src="item.avatar"></v-img>
              -->
              {{ apprLine.empNm.substr(0, 1) }}
            </v-list-item-avatar>
            <v-list-item-content>
              <v-list-item-title>{{ apprLine.empNm }} {{ apprLine.dutyNm }}</v-list-item-title>
              <v-list-item-subtitle>{{ apprLine.deptNm }}</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </template>
      </v-list>
    </v-menu>
  </div>
</template>

<script>
export default {
  props: {
    apprGrpLines: {
      type: Array,
      default: null
    }
  },
  data: () => ({
  }),
  methods: {
  }
}
</script>
