<template>
  <div id="app">
    <input type="text" v-model="city" />
    <button @click="weatherFetch()">find</button>
    <p>{{ weatherResponse }}</p>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      weatherResponse: null,
      city: 'London'
    }
  },
  async mounted() {
    await this.weatherFetch()
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
</style>
