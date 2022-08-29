<template>
  <div class="row tabelList">
    <div class="row tabelList_title">
      <div class="tabelList_title-check">

      </div>
      <div class="tabelList_title-name">
        Описание
      </div>
      <div class="tabelList_title-status">
        Статус
      </div>
      <div class="tabelList_title-date">
        Дата
      </div>
    </div>
    <row-to-do @selectWork="selectWork" :doing="doing" v-for="doing in this.todo"  :key="doing.desc">

    </row-to-do>
  </div>
</template>

<script>
import RowToDo from "@/components/rowToDo";
export default {
  name: "tabelList",
  components: {RowToDo},
  props:{
    todo:Array,
  },methods:{
    selectWork(elem){
      this.$emit('selectWorkMain', {
        elem:elem
      })
    }
  }

}
</script>

<style scoped lang="scss">

.tabelList_title{
  padding-bottom: 20px!important;
  padding-top: 20px!important;
  @media(max-width: 768px){
    display: none;
  }
  &>*{
    font-family: VelaSans;
    color: #16191D;
    font-weight: 400;
    font-size: 14px;
  }
  &-check{
    border-right: 1px solid #C4C4C4;
    width: 10%;
    height: 100%;
  }
  &-date,&-status{
    width: 15%;
    border-left: 1px solid #C4C4C4;
  }
  &-name{
    width: 60%;
  }
}
</style>