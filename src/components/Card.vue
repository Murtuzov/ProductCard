<template>
  <div class="card__item">
    <div class="hover">
      <div class="card__item-edit">
        <img src="./images/Edit.svg" alt="Delete">
      </div>
      <div class="card__item-delete" @click="$emit('deleteCard' , card)">
        <img src="./images/Delete.svg" alt="Delete">
      </div>
    </div>

    <img :src="card.image" alt="Изображение товара" class="card__item-img">
    <div class="card__item-text">
      <h6>{{ card.name }}</h6>
      <p>{{card.description}}</p>
      <h5>{{card.price + " руб."}}</h5>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    card:{
        type: Object,
    }
  },

}
</script>

<style scoped>
  .card__item{
    /*width: calc(33% - 16px);*/
    max-width: 332px;
    width: 100%;
    height: 423px;
    background: #FFFEFB;
    box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    color: #3F3F3F;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    position: relative;
  }
  .hover{
    display: flex;
    position: absolute;
    gap: 5px;
    right:  -10px;
    top: -10px;
  }
  .card__item:hover .card__item-delete{
    display: flex;
  }
  .card__item:hover .card__item-edit{
    display: flex;
  }
  .card__item-delete{
    width: 32px;
    height: 32px;
    background: #FF8484;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    justify-content: center;
    align-content: center;
    flex-wrap: wrap;
    right:  -10px;
    top: -10px;
    display: none;
  }

  .card__item-edit{
    width: 32px;
    height: 32px;
    background: #7BAE73;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    justify-content: center;
    display: none;
    align-content: center;
    flex-wrap: wrap;
    right:  -10px;
    top: -10px;
  }
  .card__item-edit > img {
    width: 16px;
    height: 16px;
  }

  .card__item-text{
    /*z-index: 999;*/
    /*position: relative;*/
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    width: 100%;
    max-width: 300px;
    height: 223px;
  }
  .card__item-text > p{
    max-width: 300px;
    overflow: hidden;
    height: 80px;
  }
  .card__item-text > h6{
    font-size: 20px;
  }
  .card__item-text > h5{
    font-size: 24px;
  }
  .card__item-img{
    height: 200px;
    width: 100%;
    object-fit: cover;
  }
</style>