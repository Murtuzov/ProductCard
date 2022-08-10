<template>
    <select v-model="selectValue" @change="changeOption">
      <option disabled value="">Выберите из списка</option>
      <option
          v-for="option in options"
          :key="option.value"
          :value="option.value"
      >
        {{option.name}}
      </option>
    </select>
</template>

<script>
export default {
  name: "my-select",
  props:{
    selectValue:{
      type: String
    },
    options:{
        type: Array
    }
  },
  methods:{
    changeOption(event){
      this.$emit('selectValue', event.target.value)
    }
  }
}

</script>

<style scoped>

</style>