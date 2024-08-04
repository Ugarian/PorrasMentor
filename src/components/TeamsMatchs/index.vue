<script setup>
  defineProps({
    teams: Array
  })
  const emit = defineEmits([
      'winner'
  ])
</script>

<template>
  <div
      v-for="team in teams"
      class="teams"
  >
    <p>{{ team.country_name }}</p>
    <img class="logo" :src="team.country_logo" />
    <button @click="emit('winner', team.country_name)">
      GANADOR
    </button>
  </div>
</template>

<style scoped>
  .teams {
    display: flex;
    flex-direction: column;
  }

  .logo {
    max-width: 30px;
    max-height: 30px;
  }
</style>