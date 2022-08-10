<template>
  <div class="card" v-if="cards.length > 0">
    <transition-group name="cardItem" class="card" style="padding: 0">
      <Card
          v-for="card in cards"
          :card="card"
          :key="card.id"
          @deleteCard="$emit('deleteCard', card)"
      />
    </transition-group>
  </div>
  <h2 v-else style="align-self: flex-start">Список товаров пуст</h2>
</template>

<script>
import Card from "@/components/Card";
export default {
  components: {Card},
  props:{
    cards:{
      type: Array,
    }
  },
}
</script>

<style scoped>
.card{
  width: 100%;
  max-width: 1028px;
  /*background: red;*/
  /*height: 30px;*/
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  /*position: relative;*/
  /*justify-content: space-around;*/
}

.cardItem-item {
  display: inline-block;
  margin-right: 10px;

}
.cardItem-enter-active, .cardItem-leave-active {
  transition: all 0.3s;
}
.cardItem-enter, .cardItem-leave-to /* .list-leave-active до версии 2.1.8 */ {
  opacity: 0;
  transform: scale(0);
}
.cardItem-move {
  transition: transform 0.5s;
}
</style>