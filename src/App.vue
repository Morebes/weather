<template>
  <div id="app">
    <div class="row">
      <div class="input-field col s12 m12 offset-l2 l8 offset-xl3 xl6">
        <input
          value="Alvin"
          id="first_name2"
          type="text"
          v-model="city"
          class="center"
          @keyup.enter="weatherFetch()"
        />
        <label class="active" for="first_name2">City</label>
        <a
          class="waves-effect col offset-s3 s6 waves-light btn"
          @click="weatherFetch()"
        >
          button
        </a>
      </div>
    </div>

    <AppLoader v-if="loading" class="center"></AppLoader>

    <WeatherCard
      v-else-if="weatherResponse.cod === 200"
      :weatherResponse="weatherResponse"
    ></WeatherCard>

    <div v-else class="center err">
      УПС... Что то пошло не так
      <div>Error - {{ weatherResponse.message }}</div>
    </div>
  </div>
</template>

<script>
import WeatherCard from '@/components/WeatherCard'

export default {
  name: 'app',
  components: { WeatherCard },
  data() {
    return {
      city: 'London',
      cityFalid: true,
      loading: true,
      weatherResponse: null
    }
  },
  async mounted() {
    await this.weatherFetch()

    this.loading = false
  },
  methods: {
    async weatherFetch() {
      const key = process.env.VUE_APP_API_KEY

      this.weatherResponse = await fetch(
        `http://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&APPID=${key}`
      ).then(r => r.json())
    }
  }
}
</script>

<style lang="sass">
@import '~materialize-css/dist/css/materialize.min.css'

body
  box-sizing: border-box
  background: url(assets/bg2.jpg) no-repeat
  color: #fff
  font-size: 24px
input
  color: #fff
.err
  font-size: 50px

  background: rgba(242, 237, 237, 0.3)
  width: 50%
  border-radius: 20px
  margin: 0 auto
  margin-top: 150px
</style>
