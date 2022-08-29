<template>
<div class="row  search justify-content-between align-items-center  ">
  <div class="col-auto search_icon">
    <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 18 18" fill="none">
      <path d="M12.8645 11.3208H12.0515L11.7633 11.0429C12.7719 9.86964 13.3791 8.34648 13.3791 6.68954C13.3791 2.99485 10.3842 0 6.68954 0C2.99485 0 0 2.99485 0 6.68954C0 10.3842 2.99485 13.3791 6.68954 13.3791C8.34648 13.3791 9.86964 12.7719 11.0429 11.7633L11.3208 12.0515V12.8645L16.4666 18L18 16.4666L12.8645 11.3208ZM6.68954 11.3208C4.12693 11.3208 2.05832 9.25214 2.05832 6.68954C2.05832 4.12693 4.12693 2.05832 6.68954 2.05832C9.25214 2.05832 11.3208 4.12693 11.3208 6.68954C11.3208 9.25214 9.25214 11.3208 6.68954 11.3208Z" fill="#59BBA6"/>
    </svg>
  </div>
  <div class=" p-0 search_input">
    <input v-model="searchQ" type="text" placeholder="Поиск Имени, статуса или даты">
  </div>
  <div class="col-auto search_sort ">
      <select-sort></select-sort>
  </div>

</div>
</template>

<script>
import SelectSort from "@/components/selectSort";
export default {
  name: "searchInput",
  components: {SelectSort},
  data:() => ({
    searchQ:'',
  })
}
</script>

<style  lang="scss">
input{
border: 1px solid transparent;
  outline: none!important;
}
.search{
  &_icon{
    width: 18px;
    max-width: 18px;
  }
  &_sort{
    max-width: 50px;
    width: 100%;
    &>*{
      font-family: VelaSans;
    }

  }
  &_input{
    flex:1;
    & input{
      width: 100%  ;
    }
  }


}
@font-face {
  font-family: 'VelaSans';
  src: local('VelaSans'), local('VelaSans'),
  url('~@/assets/VelaSans-Regular.woff') format('woff'),
  url('~@/assets/VelaSans-Regular.woff2') format('woff2');
  font-weight: 400;
  font-style: normal;
}
</style>