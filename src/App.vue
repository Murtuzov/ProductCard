<template>
  <div class="app">
    <header id="header">
      <h1 class="header-title">Добавление товара</h1>
      <div class="header-sort">
        <input placeholder="Поиск…" type="search" v-model="searchQuery" class="header-search">
        <select v-model="selectedSort" class="header-filter">
          <option disabled value="">Выберите из списка</option>
          <option
              v-for="option in sortOptions"
              :key="option.value"
              :value="option.value"
          >
              {{option.name}}
          </option>
        </select>
      </div>
    </header>
    <div class="wrapper">
      <form-cards
        @create="add"
      />
        <card-list
            :cards="sortedAndSearchCard"
            @deleteCard="removeCard"
        />
    </div>
  </div>
</template>

<script>
import FormCards from "@/components/FormCards";
import CardList from "@/components/CardList";
export default {
  components: {
    CardList, FormCards,
  },

  data(){
    return{
      cards: [
        {id: 1, name: "явание товара", description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк", image: "https://img.desktopwallpapers.ru/auto/pics/wide/1920x1200/f8e101812b260e55d1d9b7aa64af8171.jpg", price: 11000},
        {id: 2, name: "ование товара", description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк", image: "https://bipbap.ru/wp-content/uploads/2017/09/1164905.jpg", price: 10000},
        {id: 3, name: "Наименование товара", description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк", image: "https://static.ngs.ru/news/99/preview/33a71cee3670e5855cab6ef6e9c6e5500f22807a_1196.jpg", price: 12000}
      ],
      selectedSort: '',
      searchQuery: '',
      sortOptions:[
        {value: 'name', name: 'По названию'},
        {value: 'maxPrice', name: 'По цене max'},
        {value: 'minPrice', name: 'По цене min'},
       ]
      }
    },
    methods: {
      add(card) {
          this.cards.push(card)
      },
      removeCard(card){
        this.cards = this.cards.filter(t => t.id !== card.id)
      },
    },
    computed:{
      sortedCard(){
        if(this.selectedSort !== 'maxPrice' && this.selectedSort !== 'minPrice') {
         return  [...this.cards].sort((elem1, elem2) => elem1[this.selectedSort]?.localeCompare(elem2[this.selectedSort]))
        }
        else if(this.selectedSort === 'maxPrice'){
          return [...this.cards].sort((elem1,elem2) => elem2['price'] - elem1['price'])
        }
        else if(this.selectedSort === 'minPrice'){
          return [...this.cards].sort((elem1,elem2) => elem1['price'] - elem2['price'])
        }
      },
      sortedAndSearchCard(){
        return this.sortedCard.filter(card => card.name.toLowerCase().includes(this.searchQuery.toLowerCase()))
      }
    }
  }
</script>

<style src="./style.css"></style>
