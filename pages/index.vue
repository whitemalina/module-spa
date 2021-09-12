<template>
  <div class="body">
    <nav>
      <div class="nav-logo">
        <img src="img/logo.svg" alt="logo">
      </div>
      <div class="nav-menu">
        <button @click="() => {
          this.planes = []
          this.planesBack = []
          this.booking = false
          this.bookingManage = false
          this.signin = false
          this.signup = false

        }
        " class="btnb profile-signup">
          Поиск
        </button>
      </div>
      <div class="nav-profile">
        <button @click="() => {
          this.planes = []
          this.planesBack = []
          this.booking = false
          this.bookingManage = false
          this.signin = false
          this.signup = true

        }" class="btnb profile-signup">
          Регистрация
        </button>
        <button @click="() => {
          this.planes = []
          this.planesBack = []
          this.booking = false
          this.bookingManage = false
          this.signin = true
          this.signup = false

        }" class="btnb btnb-light profile-signin">
          Вход
        </button>
      </div>
    </nav>
    <main>

      <!--        Бронирование-->
      <transition name="fade-down">
        <span style="margin: 0 auto;" v-if="booking === true">
          <container title="Выбранные рейсы">
           <div :key="index" v-for="(item, index) in this.planes" v-if="item.selected">
             <div class="input-control">
               <span class="input-pass">{{ item.flight }} | {{ item.aircraft }}</span>
             </div>
             <div v-model="selected" class="form-wrapper">
               <div class="form-city">
                 <div class="form-from" v-bind:class="{ selected: item.selected}">

                   <div class="title">{{ item.date }}</div>
                   <span class="input-from">{{ item.time[0] }}:{{ item.time[1] }} | {{ item.cityFrom }}</span>
                 </div>
                 <div class="form-divider"></div>
                 <div class="form-to" v-bind:class="{ selected: item.selected}">
                   <div class="title">{{ item.date }}</div>
                   <span
                       class="input-from">{{ item.arrivalTime[0] }}:{{ item.arrivalTime[1] }} | {{ item.cityTo }}</span>
                 </div>
               </div>
               <div class="form-dates" v-bind:class="{ selected: item.selected}">
                 <div class="form-dep">
                   <div class="title">Время в пути</div>
                   <span class="input-dep">{{ item.flightTime }} ч</span>
                 </div>
                 <div class="form-back">
                   <div class="title">Стоимость</div>
                   <span class="input-back">{{ item.cost }} ₽</span>
                 </div>
               </div>
             </div>
           </div>
           <div :key="index" v-for="(item, index) in this.planesBack" v-if="item.selected">
             <div class="input-control">
               <span class="input-pass">{{ item.flight }} | {{ item.aircraft }}</span>
             </div>
             <div v-model="selected" class="form-wrapper">
               <div class="form-city">
                 <div class="form-from" v-bind:class="{ selected: item.selected}">

                   <div class="title">{{ item.date }}</div>
                   <span class="input-from">{{ item.time[0] }}:{{ item.time[1] }} | {{ item.cityFrom }}</span>
                 </div>
                 <div class="form-divider"></div>
                 <div class="form-to" v-bind:class="{ selected: item.selected}">
                   <div class="title">{{ item.date }}</div>
                   <span
                       class="input-from">{{ item.arrivalTime[0] }}:{{ item.arrivalTime[1] }} | {{ item.cityTo }}</span>
                 </div>
               </div>
               <div class="form-dates" v-bind:class="{ selected: item.selected}">
                 <div class="form-dep">
                   <div class="title">Время в пути</div>
                   <span class="input-dep">{{ item.flightTime }} ч</span>
                 </div>
                 <div class="form-back">
                   <div class="title">Стоимость</div>
                   <span class="input-back">{{ item.cost }} ₽</span>
                 </div>
               </div>
             </div>
           </div>
            <button @click="goBookingManage" class="form-btn">Продолжить <i class="arrow right"></i></button>
         </container>
          <container style="margin-top: 60px;" title="Пассажиры">
          <transition-group name="fade-up">
          <div :key="index" class="passanger" v-for="(item, index) in bookingPass">
            <input type="text" placeholder="Имя" class="passInput" v-model="item.name">
            <input type="text" placeholder="Фамилия" class="passInput" v-model="item.lastName">
            <input type="text" placeholder="Дата рождения" class="passInput" v-model="item.date">
            <input type="text" placeholder="Номер документа" class="passInput" v-model="item.document">
            <button class="passDel" v-if="bookingPass.length > 1" @click="delPass(index)">X</button>
          </div>
            </transition-group>
          <button @click="passAdd" class="form-btn">Новый пассажир  +</button>
        </container>
        </span>
      </transition>

      <!--      Управление бронированием-->
      <transition name="fade-down">
        <span style="margin: 0 auto;" v-if="bookingManage === true">
          <container title="Выбранные рейсы">
             <div :key="index" v-for="(item, index) in this.planes" v-if="item.selected">
               <div class="input-control">
                 <span class="input-pass">{{ item.flight }} | {{ item.aircraft }}</span>
               </div>
               <div v-model="selected" class="form-wrapper">
                 <div class="form-city">
                   <div class="form-from" v-bind:class="{ selected: item.selected}">

                     <div class="title">{{ item.date }}</div>
                     <span class="input-from">{{ item.time[0] }}:{{ item.time[1] }} | {{ item.cityFrom }}</span>
                   </div>
                   <div class="form-divider"></div>
                   <div class="form-to" v-bind:class="{ selected: item.selected}">
                     <div class="title">{{ item.date }}</div>
                     <span
                         class="input-from">{{ item.arrivalTime[0] }}:{{ item.arrivalTime[1] }} | {{ item.cityTo }}</span>
                   </div>
                 </div>
                 <div class="form-dates" v-bind:class="{ selected: item.selected}">
                   <div class="form-dep">
                     <div class="title">Время в пути</div>
                     <span class="input-dep">{{ item.flightTime }} ч</span>
                   </div>
                   <div class="form-back">
                     <div class="title">Стоимость</div>
                     <span class="input-back">{{ item.cost }} ₽</span>
                   </div>
                 </div>
               </div>
             </div>
             <div :key="index" v-for="(item, index) in this.planesBack" v-if="item.selected">
               <div class="input-control">
                 <span class="input-pass">{{ item.flight }} | {{ item.aircraft }}</span>
               </div>
               <div v-model="selected" class="form-wrapper">
                 <div class="form-city">
                   <div class="form-from" v-bind:class="{ selected: item.selected}">

                     <div class="title">{{ item.date }}</div>
                     <span class="input-from">{{ item.time[0] }}:{{ item.time[1] }} | {{ item.cityFrom }}</span>
                   </div>
                   <div class="form-divider"></div>
                   <div class="form-to" v-bind:class="{ selected: item.selected}">
                     <div class="title">{{ item.date }}</div>
                     <span
                         class="input-from">{{ item.arrivalTime[0] }}:{{ item.arrivalTime[1] }} | {{ item.cityTo }}</span>
                   </div>
                 </div>
                 <div class="form-dates" v-bind:class="{ selected: item.selected}">
                   <div class="form-dep">
                     <div class="title">Время в пути</div>
                     <span class="input-dep">{{ item.flightTime }} ч</span>
                   </div>
                   <div class="form-back">
                     <div class="title">Стоимость</div>
                     <span class="input-back">{{ item.cost }} ₽</span>
                   </div>
                 </div>
               </div>
             </div>
             <div class="bookingInfo">
               Код бронирования <br>
               <span>{{bookingCode}}</span> <br>
               Стоимость бронирования <br>
               <span>{{bookingCost}}</span> ₽
             </div>
             <button @click="() => {
          this.planes = []
          this.planesBack = []
          this.booking = false
          this.bookingManage = false
          this.signin = false
          this.signup = false

        }" class="form-btn">Продолжить <i class="arrow right"></i></button>
         </container>
          <container style="margin-top: 60px;" title="Пассажиры">
          <transition-group name="fade-up">
          <div :key="index" class="passanger" v-for="(item, index) in bookingPass">
            <input type="text" placeholder="Имя" class="passInput" v-model="item.name">
            <input type="text" placeholder="Фамилия" class="passInput" v-model="item.lastName">
            <input type="text" placeholder="Дата рождения" class="passInput" v-model="item.date">
            <input type="text" placeholder="Номер документа" class="passInput" v-model="item.document">
          </div>
            </transition-group>
        </container>
        </span>
      </transition>

      <!--     Найденные рейсы -->
      <transition name="fade-down" v-if="booking !== true">
        <container v-if="planes.length > 0 && bookingManage === false" title="Найденные рейсы">
          <div :key="index" v-for="(item, index) in this.planes" @click="item.selected=!item.selected">
            <div class="input-control">
              <span class="input-pass">{{ item.flight }} | {{ item.aircraft }}</span>
            </div>
            <div v-model="selected" class="form-wrapper">
              <div class="form-city">
                <div class="form-from" v-bind:class="{ selected: item.selected}">

                  <div class="title">{{ item.date }}</div>
                  <span class="input-from">{{ item.time[0] }}:{{ item.time[1] }} | {{ item.cityFrom }}</span>
                </div>
                <div class="form-divider"></div>
                <div class="form-to" v-bind:class="{ selected: item.selected}">
                  <div class="title">{{ item.date }}</div>
                  <span
                      class="input-from">{{ item.arrivalTime[0] }}:{{ item.arrivalTime[1] }} | {{ item.cityTo }}</span>
                </div>
              </div>
              <div class="form-dates" v-bind:class="{ selected: item.selected}">
                <div class="form-dep">
                  <div class="title">Время в пути</div>
                  <span class="input-dep">{{ item.flightTime }} ч</span>
                </div>
                <div class="form-back">
                  <div class="title">Стоимость</div>
                  <span class="input-back">{{ item.cost }} ₽</span>
                </div>
              </div>
            </div>
          </div>
          <div :key="index" v-for="(item, index) in this.planesBack" @click="item.selected=!item.selected">
            <div class="input-control">
              <span class="input-pass">{{ item.flight }} | {{ item.aircraft }}</span>
            </div>
            <div v-model="selected" class="form-wrapper">
              <div class="form-city">
                <div class="form-from" v-bind:class="{ selected: item.selected}">
                  <div class="title">{{ item.date }}</div>
                  <span class="input-from">{{ item.time[0] }}:{{ item.time[1] }} | {{ item.cityFrom }}</span>
                </div>
                <div class="form-divider"></div>
                <div class="form-to" v-bind:class="{ selected: item.selected}">
                  <div class="title">{{ item.date }}</div>
                  <span
                      class="input-from">{{ item.arrivalTime[0] }}:{{ item.arrivalTime[1] }} | {{ item.cityTo }}</span>
                </div>
              </div>
              <div class="form-dates" v-bind:class="{ selected: item.selected}">
                <div class="form-dep">
                  <div class="title">Время в пути</div>
                  <span class="input-dep">{{ item.flightTime }} ч</span>
                </div>
                <div class="form-back">
                  <div class="title">Стоимость</div>
                  <span class="input-back">{{ item.cost }} ₽</span>
                </div>
              </div>
            </div>
          </div>
          <button @click="goBooking" class="form-btn">Перейти к бронированию <i class="arrow right"></i></button>
        </container>
      </transition>

      <!--     Логин -->
      <transition name="fade-down" >
        <container v-if="signin === true && signup !== true" title="Вход">
          <input type="text" class="signinInput" placeholder="Логин">
          <input type="text" class="signinInput" placeholder="Пароль">
          <button @click="() => {
          this.planes = []
          this.planesBack = []
          this.booking = false
          this.bookingManage = false
          this.signin = false

        }" class="form-btn">Войти <i class="arrow right"></i></button>
        </container>
      </transition>

      <!--     Регистрация -->
      <transition name="fade-down" >
        <container v-if="signup === true && signin === false" title="Регистрация">
          <input type="text" class="signinInput" placeholder="Логин">
          <input type="text" class="signinInput" placeholder="Пароль">
          <input type="text" class="signinInput" placeholder="Подтверждение пароля">
          <button @click="() => {
          this.planes = []
          this.planesBack = []
          this.booking = false
          this.bookingManage = false
          this.signin = false

        }" class="form-btn">Войти <i class="arrow right"></i></button>
        </container>
      </transition>

      <!--        Главная тайтл-->
      <transition name="fade-down">
        <div v-if="planes.length === 0 && signin !== true && signup !== true" class="title">
          Поиск и покупка <br> авиабилетов
        </div>
      </transition>

      <!--        Поиск-->
      <transition name="fade-up">
        <div v-if="planes.length === 0 && signin !== true && signup !== true" class="search-wrapper">
          <div class="search-container">

            <div class="input-control">
              <select class="input-pass" v-model="searchInput.passenger">
                <option value="1">
                  1 пассажир
                </option>
                <option value="2">
                  2 пассажира
                </option>
                <option value="3">
                  3 пассажира
                </option>
                <option value="4">
                  4 пассажира
                </option>
                <option value="5">
                  5 пассажиров
                </option>
                <option value="6">
                  6 пассажиров
                </option>
                <option value="7">
                  7 пассажиров
                </option>
                <option value="8">
                  8 пассажиров
                </option>
              </select>
            </div>
            <div class="form-wrapper">
              <div class="form-city">
                <div class="form-from">
                  <div class="title">ОТКУДА</div>
                  <input type="text" v-model="searchInput.fromInput" class="input-from">
                </div>
                <div class="form-divider"></div>
                <div class="form-to">
                  <div class="title">КУДА</div>
                  <input type="text" v-model="searchInput.toInput" class="input-to">
                </div>
              </div>
              <div class="form-dates">
                <div class="form-dep">
                  <div class="title">ТУДА</div>
                  <input type="date" v-model="searchInput.dateTo" class="input-dep">
                </div>
                <div class="form-back">
                  <div class="title">ОБРАТНО</div>
                  <input type="date" v-model="searchInput.dateBack" class="input-back">
                </div>
              </div>
            </div>
            <button @click="search" class="form-btn">Найти билеты <i class="arrow right"></i></button>
          </div>
        </div>
      </transition>



    </main>

    <div data-relative-input="true" id="scene">
      <div data-depth="0.4" class="cool">
        <img src="img/bg.svg" alt="bg">
      </div>
      <div data-depth="0.2" class="cool cool-bottom">
        <img src="img/bg.svg" alt="bg-bottom">
      </div>
    </div>
  </div>
</template>

<style lang="sass">
.signinInput
  padding: 15px 25px
  margin: 8px
  background: none
  border-radius: 8px
  border: 1px dashed #707070
  &:focus
    outline: none
.bookingInfo
  margin-top: 15px
  span
    font-size: 1.5em
.passInput
  padding: 5px 10px
  margin: 8px

  background: none
  border: none
  //border-radius: 8px
  border: none
  border-bottom: 1px dashed #707070

  &:focus
    outline: none

.passDel
  background: none
  color: #707070
  border: none
  font-weight: 500

  &:focus
    outline: none

.passAdd
  background: none
  color: #707070
  border: none
  font-weight: 500

  &:focus
    outline: none

.selected
  border: 2px solid #707070 !important

.fade-down-enter-active, .fade-down-leave-active
  transition: .5s

.fade-down-enter, .fade-down-leave-to
  transform: translateY(-100%)
  opacity: 0

.fade-up-enter-active, .fade-up-leave-active
  transition: .5s

.fade-up-enter, .fade-up-leave-to
  transform: translateY(100%)
  opacity: 0


@import url('https://fonts.googleapis.com/css2?family=Oswald:wght@300;400;500;700&display=swap')
*
  font-family: 'Oswald', sans-serif

.body
  position: relative
  overflow: hidden
  height: 100vh
  background: rgba(40, 40, 40, 0.06)

  #scene
    position: absolute
    top: 0
    right: 0
    width: 100vw
    height: 100vh
    z-index: -1
    overflow: hidden

    .cool
      position: absolute
      width: 100%
      height: 100%
      filter: blur(7px) saturate(200%)
      opacity: 0.5

      img
        transform: translate(30%, -30%)

      &-bottom
        img
          transform: translate(-10%, 70%) rotate(180deg)

    img
      width: 100%
      height: 100%

.btnb
  color: #303030
  border-radius: 15px
  font-weight: 400
  font-size: 1.1em
  padding: 5px 25px
  margin: 0.3em
  transition: 0.4s
  background: none
  border: 1px solid rgba(0, 0, 0, 0)

  &:hover
    color: rgba(0, 0, 0, 0.53)

  &-light
    border: 1px solid #303030

nav
  padding: 35px 60px
  min-height: 60px
  width: 100%
  display: flex
  align-items: center
  justify-content: start

  .nav-logo
    img
      max-height: 45px

  .nav-profile
    display: flex
    align-items: center
    flex-wrap: wrap
    justify-content: center
    margin-left: auto

  .nav-menu
    display: flex
    align-items: center
    flex-wrap: wrap
    justify-content: center
    margin-left: auto

main
  width: 100%
  height: calc(100vh - 120px)
  padding: 35px 75px
  display: flex
  flex-direction: column
  align-items: start
  justify-content: flex-start

  .title
    line-height: 50px
    margin: 0.5em 1em
    font-size: 3.5rem
    color: rgba(41, 41, 41, 0.94)
    font-weight: 500
    position: absolute

  .search-wrapper
    display: flex
    justify-content: center
    align-items: center
    margin-top: auto
    width: 100%
    padding: 1em 1em 5em 1em

  .search-container
    position: relative
    min-width: 50%
    display: inline-block
    border-radius: 25px
    padding: 35px 35px 50px
    background: rgba(255, 255, 255, 0.85)

    .input-pass
      background: none
      border: none
      font-weight: 300
      color: #707070
      margin-bottom: 5px

    .form-btn
      background: #151515
      color: white
      padding: 15px 32px
      border-radius: 10px
      border: none
      position: absolute
      right: calc(35px + 1em)
      bottom: 0
      transform: translateY(50%)

      &:hover
        .arrow
          transform: translateX(10px) rotate(-45deg) translateY(-1px)

      .arrow
        border: solid #ffffff
        border-width: 0 3px 3px 0
        display: inline-block
        padding: 3px
        transition: .3s

      .right
        transform: rotate(-45deg) translateY(-1px)
        margin-left: 10px

  .form-wrapper
    display: flex
    justify-content: start
    align-items: start
    flex-wrap: wrap

    .title
      font-size: 0.8em
      color: rgba(0, 0, 0, 0.73)
      line-height: 1em
      margin: 0 0 5px
      font-weight: normal
      position: relative

    .form-city
      text-align: left
      display: flex
      justify-content: start
      align-items: start
      margin-right: 1em
      margin-top: 0.5em

      .form-from, .form-to
        border: 1px dashed #707070
        border-radius: 10px
        padding: 20px 70px 20px 25px

        input
          border: none
          border-bottom: 1px dashed #242424
          transition: .5s

          background: none

          &:focus
            outline: none
            border-bottom: 1px solid #242424

      .form-divider
        width: 20px

        background: #323131
        height: 1px
        margin: auto 0


    .form-dates
      margin-right: 1em
      border-radius: 10px
      border: 1px dashed #707070
      background: none
      margin-top: 0.5em
      text-align: left
      display: flex
      justify-content: start
      align-items: start

      .form-dep, .form-back
        padding: 20px 20px 20px 25px

        input
          border: none
          border-bottom: 1px dashed #242424
          font-weight: 300
          background: none

          &:focus
            outline: none

.form-btn
  background: #151515
  color: white
  padding: 15px 32px
  border-radius: 10px
  border: none
  position: absolute
  right: calc(35px + 1em)
  bottom: 0
  transform: translateY(50%)

  &:hover
    .arrow
      transform: translateX(10px) rotate(-45deg) translateY(-1px)

  .arrow
    border: solid #ffffff
    border-width: 0 3px 3px 0
    display: inline-block
    padding: 3px
    transition: .3s

  .right
    transform: rotate(-45deg) translateY(-1px)
    margin-left: 10px

</style>
<script>
import Parallax from "parallax-js";

let faker = require('faker');

function getRandom(min, max) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

export default {
  name: "index",
  components: {},
  data() {
    return {
      signup: false,
      signin : false,
      bgVars: {
        offsetY: 10,
        offsetX: 50,
        filter: 1.3
      },
      searchInput: {
        fromInput: "",
        toInput: "",
        dateTo: "",
        dateBack: "",
        passenger: 1
      },
      planes: [],
      planesBack: [],
      selected: [],
      booking: false,
      bookingPass: [],
      bookingManage: false,
      bookingCode: '',
      bookingCost: '',
      aircrafts: ["Utair", "Pobeda", "S7"]
    };
  },
  methods: {
    passAdd() {
      this.bookingPass = [...this.bookingPass, {
        name: '',
        lastName: '',
        date: '',
        document: ''
      }]
    },
    delPass(index) {
      this.bookingPass.splice(index, 1);
    },
    search() {
        this.planes = []
        this.planesBack = []
        this.booking = false
        this.bookingManage = false
        this.signin = false
      for (let i = 0; i < this.searchInput.passenger; i++) {
        this.bookingPass = [...this.bookingPass, {
          name: '',
          lastName: '',
          date: '',
          document: ''
        }]
      }
      for (let i = 0; i < getRandom(1, 3); i++) {
        let time = [getRandom(10, 19), getRandom(10, 59)]
        let flightTime = getRandom(1, 5)

        this.planes = [...this.planes, {
          flight: "Р" + getRandom(100, 999),
          aircraft: this.aircrafts[getRandom(0, 2)],
          time: time,
          flightTime: flightTime,
          cost: getRandom(10000, 19092) * this.searchInput.passenger,
          arrivalTime: [time[0] + flightTime, time[1]],
          selected: false,
          from: this.searchInput.fromInput,
          to: this.searchInput.toInput,
          date: this.searchInput.dateTo,
          cityTo: this.searchInput.toInput,
          cityFrom: this.searchInput.fromInput
        }]
      }
      if (this.searchInput.dateBack !== "") {
        let time = [getRandom(10, 19), getRandom(10, 59)]
        let flightTime = getRandom(1, 5)
        for (let i = 0; i < getRandom(1, 3); i++) {
          this.planesBack = [...this.planesBack, {
            flight: "Р" + getRandom(100, 999),
            aircraft: this.aircrafts[getRandom(0, 2)],
            time: time,
            flightTime: flightTime,
            cost: getRandom(10000, 19092) * this.searchInput.passenger,
            arrivalTime: [time[0] + flightTime, time[1]],
            selected: false,
            from: this.searchInput.toInput,
            to: this.searchInput.fromInput,
            date: this.searchInput.dateBack,
            cityFrom: this.searchInput.toInput,
            cityTo: this.searchInput.fromInput
          }]
        }
      }
    },
    goBooking() {
      this.booking = !this.booking
    },
    goBookingManage() {
      this.booking = !this.booking
      this.bookingManage =!this.booking
      this.bookingCode = 'B'+ getRandom(10000, 99999)
      this.bookingCost = getRandom(10000,19000) * this.bookingPass.length

    }
  },

  mounted() {
    let scene = document.getElementById("scene");
    let parallaxInstance = new Parallax(scene);
  }
};
</script>
