<template>
  <v-card>
    <v-card-title>법인카드 선택</v-card-title>
    <v-card-text>
      <v-select
        :items="cards"
        item-text="cardNo"
        item-value="cardNo"
        outlined
        @change="selectCmsCard"
      />
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  data: () => ({
    cards: [
      { cardNo: '1234123412341234', state: '정상' },
      { cardNo: '5678567856785678', state: '대여' }
    ]
  }),
  methods: {
    selectCmsCard (card) {
      this.$emit('select-cms-card', card)
    }
  }
}
</script>
