<template>
  <div class="center">
    <p>{{ weatherResponse.name }}</p>
    {{ weatherResponse.coord.lon }} ,{{ weatherResponse.coord.lat }}
    <div class="temp text-format">
      <p>{{ temp }} &#8451;</p>
    </div>
    <div class="sky text-format">
      <p>{{ weatherResponse.weather[0].main }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'weatherCard',
  props: {
    weatherResponse: {
      type: Object,
      required: true
    }
  },
  computed: {
    temp() {
      return Math.round(this.weatherResponse.main.temp)
    }
  }
}
</script>

<style lang="sass" scoped>
.text-format
 font-size: 46px
 font-weight: 900
 padding: 5px

.temp
  background: rgba(242, 237, 237, 0.3)
  width: 30%
  padding: 0 5px
  border-radius: 20px
  margin: 0 auto

p
  margin: 10px
</style>
