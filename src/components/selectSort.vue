<template>
  <v-row  class="w-auto justify-center align-items-center">
       Сортировать по :

      <v-select
          @input="sortBy"
          :items="items"
          label="Дате"
          solo
          return-object
      ></v-select>
  </v-row>
</template>

<script>
export default {
  name: "selectSort",
  data() {
    return {
      items: ['Дате', 'Статусу'],
    }
  },
  methods:{
    sortBy(item){
      this.$emit(
'sortby',item
      )
    }
  }
}
</script>

<style   lang="scss">
.v-text-field, .v-input__slot {
  padding: 0px;
  margin: 0px;
}

.v-text-field__details {
  display: none !important;
}

.v-text-field > .v-input__control > .v-input__slot:before, .v-text-field > .v-input__control > .v-input__slot:after {
  border: none !important;
}

.v-text-field.v-text-field--solo:not(.v-text-field--solo-flat) > .v-input__control > .v-input__slot {
  box-shadow: none !important;
}
.v-input{
  max-width: 120px!important;
  width: 100%;
}
#app > div:nth-child(2) > div > div.col-auto.search_sort{
  min-width: 200px;
}
</style>