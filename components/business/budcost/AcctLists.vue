<template>
  <v-list>
    <v-list-item-group>
      <v-list-item
        v-for="(acct, i) in accts"
        :key="i"
        @click="selectAcct(acct)"
      >
        <v-list-item-content>
          <v-list-item-title>{{ acct.title }}</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list-item-group>
  </v-list>
</template>

<script>
export default {
  data: () => ({
    accts: [
      { title: '여비교통-산교통비.외근' }
    ]
  }),
  methods: {
    selectAcct (acct) {
      this.$emit('select-acct', acct)
    }
  }
}
</script>
