<script setup>
  import Teams from './components/TeamsMatchs/index.vue'
  import {computed, ref} from "vue"
  import teamsMock from '@/imposters/teams.json'

  const winner = ref('')
  const teams = ref([])

  const setWinner = (team) => {
    winner.value = team
  }

  const params = {
    met: 'Countries',
    APIkey: 'ffa5a6da51b88f1b9e2eeb6f4d41ad00ee01b9d5214264a0838dd5dc322090b8'
  }
  /* fetch(`https://apiv2.allsportsapi.com/football/?met=${params.met}&APIkey=${params.APIkey}`)
    .then((res) => res.json())
    .then((data) => {
      console.log(data)
      teams.value = data.result
    }) */
  teams.value = teamsMock
  const addPagination = 10
  const paginationStart = ref(0)

  const paginatedTeams = computed(() => teams.value.slice(paginationStart.value, paginationEnds.value))
  const paginationEnds = computed(() => paginationStart.value + addPagination)
  const nextPage = () => {
    if (paginationEnds.value < teams.value.length) paginationStart.value += addPagination
  }
  const previousPage = () => {
    if (paginationStart.value > 0) paginationStart.value -= addPagination
  }

</script>

<template>
  <p>Equipo ganador: {{ winner }} </p>
  <br>
  <button
      @click="previousPage"
      :disabled="paginationStart <= 0"
  >
    Back
  </button>
  <button
      @click="nextPage"
      :disabled="paginationEnds >= teams.length"
  >
    Next
  </button>
  <br>
  <Teams
    :teams="paginatedTeams"
    @winner="setWinner"
  />
</template>

<style scoped>
</style>
