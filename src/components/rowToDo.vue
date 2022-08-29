<template>
  <div class="row tabelList_info ">
    <div class="tabelList_info-check">

      <div class="tabelList_info-check--checkbox " v-bind:class="{ check: doing.state }" @click="selectWork">
        <svg v-if="doing.state" xmlns='http://www.w3.org/2000/svg' height='11' width='10' viewBox='0 0 10 11'
             fill='none'>
          <path d='M1 5L5 10.5L9.5 1' stroke='#134EC1' stroke-linecap='round' stroke-linejoin='round'/>
        </svg>
      </div>
    </div>
    <div class="tabelList_info-name">
      {{ doing.desc }}
    </div>
    <div class="tabelList_info-status done" v-if="doing.state">
      Выполнено

    </div>
    <div class="tabelList_info-status inwork" v-if="!doing.state">
      В работе
    </div>

    <div class="tabelList_info-date">
      {{ doing.date }}
    </div>
  </div>
</template>

<script>
export default {
  name: "rowToDo",
  data() {
    return {
      //data here
    }
  },
  props: ['doing'],
  methods: {
    selectWork() {

      this.$emit('selectWork', {
        state: this.doing.state,
        id: this.doing.id
      })
    }
  },
}
</script>

<style scoped lang="scss">
.tabelList_info {
  padding-bottom: 20px !important;
  padding-top: 20px !important;
  @media(max-width: 625px){
    padding-left: 10px!important;
  }

  &:hover {
    background-color: #F6F9FF;
  }
  &-name{
    padding-right: 0;
    @media(max-width: 625px){
      width: auto;
      display: flex;
      align-items: center;
    }
  }
  & .v-input--selection-controls {
    padding-top: 0 !important;
    margin-top: 0 !important;
  }

  & > * {
    font-family: VelaSans;
    color: #16191D;
    font-weight: 400;
    font-size: 14px;

  }

  &-check {
    border-right: 1px solid #C4C4C4;
    width: 10%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    min-width: 20px;
    @media(max-width: 625px){
      border: none;
    }

    &--checkbox.check {
      border-radius: 50%;
      border: 1px solid #134EC1;
      width: 20px;
      height: 20px;
      min-width: 20px;
      box-shadow: 0px 4px 4px rgba(19, 78, 193, 0.15);


    }

    &--checkbox {
      display: flex;
      justify-content: center;
      align-items: center;
      border-radius: 50%;
      box-shadow: 0px 4px 4px rgba(19, 78, 193, 0.15);
      width: 20px;
      height: 20px;
      min-width: 20px;
      border: 1px solid #16191D;
    }

  }

  &-date, &-status {
    width: 15%;
    border-left: 1px solid #C4C4C4;
    @media(max-width: 625px){
      width: 50%;
      border: none;
    }
  }

  &-status.done {
    color: #134EC1;
  }

  &-status.inwork {
    color: #F89B11;
  }

  &-name {
    width: 60%;
  }
}

.theme--light.v-messages {
  display: none !important;
}

</style>