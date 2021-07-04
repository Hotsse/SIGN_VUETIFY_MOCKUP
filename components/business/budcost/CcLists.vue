<template>
  <v-list>
    <v-list-item-group>
      <v-list-item
        v-for="(cc, i) in ccs"
        :key="i"
        @click="selectCc(cc)"
      >
        <v-list-item-content>
          <v-list-item-title>{{ cc.title }}</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list-item-group>
  </v-list>
</template>

<script>
export default {
  data: () => ({
    ccs: [
      { title: '재무관리본부공통' }
    ]
  }),
  methods: {
    selectCc (cc) {
      this.$emit('select-cc', cc)
    }
  }
}
</script>
