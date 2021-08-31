<template>
  <v-row justify="center">
    <v-col cols="auto">
      <v-btn
        color="default"
        @click="goPrevStep()"
      >
        {{ prevName }}
      </v-btn>
    </v-col>
    <v-spacer />
    <v-col cols="auto">
      <v-btn
        color="primary"
        @click="goNextStep()"
      >
        {{ nextName }}
      </v-btn>
    </v-col>
  </v-row>
</template>

<script>
export default {
  props: {
    prevName: {
      type: String,
      default: '이전'
    },
    nextName: {
      type: String,
      default: '다음'
    }
  },
  data: () => ({
  }),
  methods: {
    goPrevStep () {
      this.$emit('prev-callback')
    },
    goNextStep () {
      this.$emit('next-callback')
    }
  }
}
</script>
