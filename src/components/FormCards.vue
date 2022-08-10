<template>
  <form action="#" class="form">
    <div class="inputWrapper">
      <div>
        <p class="form-title form-title_after">Наименование товара</p>
        <input
            @input="notValidateName"
            v-model.trim="card.name"
            type="text"
            class="form-input"
            placeholder="Введите наименование товара"
            :class="{
            'borderColorRed' : cardNameEmpty,
          }"
        >
        <p class="form-required" v-show="cardNameEmpty">Поле является обязательным</p>
      </div>
      <div>
        <p class="form-title">Описание товара</p>
        <textarea v-model="card.description"  class="form-input form-input_height" placeholder="Введите описание товара"></textarea>
      </div>
      <div>
        <p class="form-title form-title_after">Ссылка на изображение товара</p>
        <input
            @input="notValidateImage"
            v-model.trim="card.image"
            type="url"
            class="form-input"
            placeholder="Введите ссылку"
            :class="{
            'borderColorRed' : cardImageEmpty,
          }"
        >
        <p class="form-required" v-show="cardImageEmpty">Поле является обязательным</p>
      </div>
      <div>
        <p class="form-title form-title_after">Цена товара</p>
        <input
            @input="notValidatePrice"
            v-model.trim="card.price"
            type="number"
            class="form-input"
            placeholder="Введите цену"
            :class="{
            'borderColorRed' : cardPriceEmpty,
          }"
        >
        <p class="form-required" v-show="cardPriceEmpty">Поле является обязательным</p>
      </div>
    </div>
    <button :class="color()" type="submit" @click="add" class="form-button">Добавить товар</button>
  </form>
</template>

<script>

export default {
  data(){
    return{
      card:{
        name: '',
        description: '',
        image: '',
        price: ''
      },
      cardNameEmpty: false,
      cardImageEmpty: false,
      cardPriceEmpty: false
    }
  },
  methods:{
    add(){
      if(this.card.name.length === 0){
        this.cardNameEmpty = true
      }
      if(this.card.image.length === 0){
        this.cardImageEmpty = true
      }
      if(this.card.price.length === 0){
        this.cardPriceEmpty = true
      }
      if(this.Validate) {
        if(this.card.description === ''){
          this.card.description = 'Описание отсутствует'
        }
        this.card.id = Date.now();
        this.$emit('create', this.card);
        this.cardNameEmpty = false
        this.cardPriceEmpty = false
        this.cardImageEmpty = false
        this.card = {
          name: '',
          description: '',
          image: '',
          price: '',
        }
      }
    },
    notValidateName(){
      this.cardNameEmpty = false
    },
    notValidatePrice(){
      this.cardPriceEmpty = false
    },
    notValidateImage(){
      this.cardImageEmpty = false
    },
    color() {
      if (this.card.name.length  && this.card.image.length && this.card.price.length) {
        return 'colorGreen';
      }
    },
  },
  computed:{
    Validate(){
      return this.card.name.length  && this.card.image.length && this.card.price.length
    }

  },
}
</script>

<style scoped>
.form{
  width: 100%;
  max-width: 332px;
  height: 100vh;
  max-height: 430px;
  background: #FFFEFB;
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-bottom: 16px;
  justify-content: space-between;
}
.inputWrapper{
  width: 100%;
  max-width: 288px;
  margin-top: 10px;
  display: flex;
  flex-direction: column;
  gap: 16px;
}
.form-input{
  background: #FFFEFB;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  width: 100%;
  max-width: 285px;
  padding: 10px 0 10px 16px;
  margin-top: 5px;
  outline: none;
  border: none;
}

.form-input_height{
  height: 100vh;
  max-height: 108px;
}
.form-input::placeholder{
  color: #B4B4B4;
  font-size: 12px;
  font-family: 'Source Sans Pro', sans-serif;
}
.form-title{
  font-size: 10px;
  line-height: 13px;
  letter-spacing: -0.02em;
  color: #49485E;
}
.form-title_after::after{
  content: '';
  width: 4px;
  height: 4px;
  position: absolute;
  background: #FF8484;
  border-radius: 4px;
}
.form-button{
  background: #EEEEEE;
  border-radius: 10px;
  width: 100%;
  /*disabled: true;*/
  max-width: 285px;
  padding: 10px 0;
  border: none;
  letter-spacing: -0.02em;
  color: #B4B4B4;
  font-size: 12px;
}
.borderColorRed{
  border: 1px solid red;
}
.colorGreen{
  background: #7BAE73;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  color: white;
}
.form-required{
  font-size: 8px;
  line-height: 10px;
  /* identical to box height */

  letter-spacing: -0.02em;

  color: #FF8484;
  margin-top: 4px;
  position: absolute;
}
@media screen and (max-width: 1200px) {
  .form{
    padding-left: 10px;
    padding-right: 10px;
    padding-bottom: 16px;
    /*background-color: red;*/
  }
}
</style>