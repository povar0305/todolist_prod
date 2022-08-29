<template>
  <div id="app" data-app>
    <div class="row_title row justify-content-between align-items-center">
      <div class="col-auto px-0">
        <h2>
          To do list
        </h2>
      </div>
      <div class="col-auto px-0">
        <div class="circle" @click="showPopupMain">
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 20 20" fill="none">
            <rect x="9" width="2" height="20" fill="#314B99"/>
            <rect x="20" y="9" width="2" height="20" transform="rotate(90 20 9)" fill="#314B99"/>
          </svg>
        </div>
      </div>

    </div>
    <div class="row">
      <div class="row  search justify-content-between align-items-center  ">
        <div class="col-auto search_icon">
          <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 18 18" fill="none">
            <path
                d="M12.8645 11.3208H12.0515L11.7633 11.0429C12.7719 9.86964 13.3791 8.34648 13.3791 6.68954C13.3791 2.99485 10.3842 0 6.68954 0C2.99485 0 0 2.99485 0 6.68954C0 10.3842 2.99485 13.3791 6.68954 13.3791C8.34648 13.3791 9.86964 12.7719 11.0429 11.7633L11.3208 12.0515V12.8645L16.4666 18L18 16.4666L12.8645 11.3208ZM6.68954 11.3208C4.12693 11.3208 2.05832 9.25214 2.05832 6.68954C2.05832 4.12693 4.12693 2.05832 6.68954 2.05832C9.25214 2.05832 11.3208 4.12693 11.3208 6.68954C11.3208 9.25214 9.25214 11.3208 6.68954 11.3208Z"
                fill="#59BBA6"/>
          </svg>
        </div>
        <div class=" p-0 search_input">
          <input style="padding-left: 10px!important" @input="searching" v-model="searchQ" type="text" placeholder="Поиск Имени, статуса или даты">
        </div>
        <div class="col-auto search_sort ">
          <select-sort @sortby="sorting"></select-sort>
        </div>

      </div>
    </div>
    <tabel-list @selectWorkMain="selectWorkMain" :todo="searching()"></tabel-list>


    <!--Надо выделить в отдельный элемент-->
    <div class="popup" v-if="togglePopup">
      <div class="popup_main">
        <div class="row popup_main-row-title align-items-center justify-content-between">
          <div class="col-auto p-0"><h3>Создать новую задачу</h3></div>

          <div class="popup_close col-auto px-0 p-0" @click="hidePopupMain">
            <svg xmlns="http://www.w3.org/2000/svg" width="8" height="8" viewBox="0 0 8 8" fill="none">
              <path d="M1 1L4 4M7 7L4 4M4 4L7 1M4 4L1 7" stroke="white" stroke-linecap="round"/>
            </svg>
          </div>
        </div>

        <form class="row" >
          <p class="px-0">
            Описание
          </p>
        </form>
        <div class="row">
          <input required v-model='newDesc' type="text" placeholder="Введите описание">
        </div>
        <div class="row justify-content-center">
          <button @click="addTask">Создать</button>
        </div>
      </div>
    </div>
  </div>


</template>

<script>
import TabelList from "@/components/tabelList";
import SelectSort from "@/components/selectSort";

export default {
  name: 'App',
  components: {TabelList, SelectSort},
  data() {
    return {
      searchQ: '',
      togglePopup: false,
      todo: [
        {desc: 'Размещение новостей на сайте', state: true, date: '22.04.2022', id: 1},
        {desc: 'Внедрить Wi-fi для читателей', state: false, date: '25.03.2022', id: 2},
        {desc: 'Отредактировать раздел “Доступная среда”', state: true, date: '15.03.2022', id: 3},
        {desc: 'Презентация “Информационные технологии””', state: false, date: '15.03.2022', id: 4},
        {desc: 'Счётчики — внедрить дизайн”', state: false, date: '09.03.2022', id: 5},
        {desc: 'Сверстать новый layout”', state: false, date: '07.03.2022', id: 6},
        {desc: 'Скролл в новостях”', state: true, date: '01.03.2022', id: 7},
        {desc: 'Форма сброса пароля”', state: false, date: '25.02.2022', id: 8},
        {desc: 'Внедрение модуля Chat”', state: true, date: '20.02.2022', id: 9},
      ],
      newDesc: ''
    }
  },
  methods: {
    showPopupMain() {
      this.togglePopup = true
    },
    hidePopupMain() {
      this.togglePopup = false
    },
    sorting(sortby) {
      if (sortby == 'Дате') {
        this.todo = this.todo.sort((task1, task2) => task1['date'] > task2['date'] ? 1 : -1);

      } else if (sortby == 'Статусу') {
        this.todo = this.todo.sort((task1, task2) => task1['state'] > task2['state'] ? 1 : -1);
      }
    },
    selectWorkMain(elem) {


      let updateElement = this.todo.find(
          function (element) {
            return element.id === elem.elem.id
          }
      )
      updateElement.state=true
      localStorage.setItem('todo', JSON.stringify(this.todo))

    },
    addTask() {
      this.todo = JSON.parse(localStorage.getItem('todo'));
      this.todo.id = this.todo[this.todo.length - 1].id + 1;
      this.todo.date = new Date().toLocaleDateString();
      var newArray = {
        desc: this.newDesc,
        state: false,
        date: this.todo.date,
        id: this.todo.id
      }
      this.todo.push(newArray);
      localStorage.setItem('todo', JSON.stringify(this.todo))
      this.newDesc = ''
      this.togglePopup = false

    },
    searching() {
      return this.todo.filter(el => {
        /*console.log(el.desc.includes(this.searchQ))
        console.log(this.searchQ)*/
        if (el.desc.includes(this.searchQ)) {
          return el
        }

      })
    }
  }, mounted() {
    if (JSON.parse(localStorage.getItem('todo'))) {
      this.todo = JSON.parse(localStorage.getItem('todo'))
    } else {
      localStorage.setItem('todo', JSON.stringify(this.todo));

    }
  },


}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@700&display=swap');

$light_violet: #D6DBEB;
$hover_light_violet: #9497a2;

$blue: #314B99;
$hover_blue: #4c7cfa;

$light_blue: #F0F5FF;
$hover_light_blue: #b0ceff;
* {
  transition: 0.2s;
  outline: none;
}

#app {
  padding-top: 104px;
  max-width: 1300px;
  width: 100%;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  padding-bottom: 104px;
  @media(max-width: 625px){
    padding-top: 2rem;
    padding-bottom: 2rem;

  }
  & .row {
    padding: 0;
    margin: 0;
  }
  & .row_title,& .row_title+.row {
    @media(max-width: 1440px){
      padding-left: 10px!important;
      padding-right: 10px!important;
    }
  }
}

.px-0 {
  padding-left: 0 !important;
  padding-right: 0 !important;
}

h2 {
  font-family: 'Montserrat', sans-serif;
  font-size: 24px !important;
  width: auto;
  letter-spacing: 0em;
  text-align: left;
}

h3 {
  font-family: Montserrat;
  font-size: 18px !important;
  font-weight: 700 !important;
  text-align: left;
  margin: 0 !important;

}

p {
  font-family: VelaSans;
  color: #16191D;
  font-weight: 400;
  font-size: 14px !important;
  margin-bottom: 5px;
}

.circle {
  width: 40px;
  height: 40px;
  padding: 0;
  margin: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  background-color: $light_violet;

  &:hover {
    background-color: $hover_light_violet;
    cursor: pointer;
  }
}

.popup {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background: rgba(255, 255, 255, 0.01);
  backdrop-filter: blur(4px);
  display: flex;
  justify-content: center;
  align-items: center;

  &_main {
    background: #FFFFFF;
    width: 100%;
    max-width: 400px;
    border: 1px solid #DDE2E4;
    padding: 40px;
    box-shadow: 0px 25px 50px -12px rgba(0, 0, 0, 0.25);
    border-radius: 6px;
    @media(max-width: 625px){
      padding-left: 25px;
      padding-right: 25px;
    }
    &-row-title {
      margin-bottom: 30px !important;
    }
  }

  &_close {
    background: $blue;
    border-radius: 5px;
    width: 22px !important;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 22px;

    &:hover {
      background-color: $hover_blue;
      cursor: pointer;
    }
  }

  & input {
    width: 100%;
    background-color: transparent;
    border: 1px solid #DDE2E4;
    border-radius: 8px;
    height: 40px;
    margin-bottom: 30px;
  }

  & button {
    color: $blue;
    padding: 12px 40px;
    background-color: $light_blue;
    border-radius: 8px;
    max-width: 150px;
    margin-bottom: 10px;

    &:hover {
      background-color: $hover_light_blue;
      color: white;
    }

  }

}

#app > div.row.tabelList > div.row.tabelList_info > div.tabelList_info-check > div > div > div.v-messages.theme--light {
  display: none !important;
}


input {
  border: 1px solid transparent;
  outline: none !important;
}
#app > div:nth-child(2) > div > div.col-auto.search_sort{
  min-width: 200px;
}
.search {
  &_icon {
    width: 18px;
    max-width: 18px;
    padding-right: 10px;
  }


  &_sort {

    width: 100%;

    & > * {
      font-family: VelaSans;
    }

  }

  &_input {
    flex: 1;

    @media(max-width: 625px){
      width: calc(100% - 60px) !important;
      flex: auto;
    }

    & input {
      padding-left: 10px!important;
      width: 100%;
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
