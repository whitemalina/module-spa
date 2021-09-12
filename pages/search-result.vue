<template>
  <div>
    <navbar />
    <div class="search-result">
      <b-card
        no-body
        class="overflow-hidden"
        style="min-width: 900px;"
        border-variant="primary"
        header="Р207"
        header-bg-variant="primary"
        header-text-variant="white"
        align="center"
      >
        <b-row no-gutters>
          <b-col md="4">
            <b-card-body class="buy">
              <!-- <b-card-text>пнд 22 нояб.</b-card-text>
                <b-card-text>17:30 Осака Международный аэропорт Кансай (KIX)</b-card-text> -->
              <div>
                <b-button class="buy-button" block variant="primary" center
                  >Купить за <br />
                  5940 ₽</b-button
                >
              </div>
            </b-card-body>
          </b-col>

          <b-col md="7">
            <b-card-body>
              <div class="avia">
                <b-card-text>Utair</b-card-text>
              </div>
              <div class="about-avia">
                <div class="flight">
                  <p class="flight-time">10:00</p>
                  <div class="arrival">
                    <p class="flight-city">Нижневартовск</p>
                    <p class="flight-date">19 сен 2021, вс</p>
                  </div>
                </div>
                <div class="about-progress">
                  <p class="about-flight-time">В пути: 4ч 55м</p>
                  <b-progress></b-progress>
                </div>
                <div class="flight">
                  <p class="flight-time">12:55</p>
                  <div class="arrival">
                    <p class="flight-city">Симферополь</p>
                    <p class="flight-date">19 сен 2021, вс</p>
                  </div>
                </div>
              </div>
            </b-card-body>
          </b-col>
        </b-row>
      </b-card>
    </div>
  </div>
</template>

<style>
.card-text{
    font-size: 1.2em;
    font-weight: 400;
}
.price {
  font-size: 20px;
  font-weight: bold;
}
.search-result {
  display: flex;
  align-items: center;
  flex-direction: column;
  margin-top: 2em;
}
b-card {
  margin-top: 1em !important;
}
.about-avia {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}
.about-progress {
  margin: 0 2em;
  width: 40%;
}
.flight-time {
  font-size: 2em;
}
.flight {
  align-self: flex-start;
}
.flight-city,
.flight-date {
  color: #a0b0b9;
  margin-top: 1px;
}
.about-flight-time {
  color: #a0b0b9;
}
.arrival {
    display: block;
}
.card-text{

}
</style>
<script>
import navbar from "@/components/navbar";
import Navbar from "../components/navbar.vue";
export default {
  name: "index",
  components: {
    navbar
  },
  data() {
    return {};
  },
  mounted() {}
};
</script>
