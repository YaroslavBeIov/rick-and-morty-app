<template>
  <div class="character-card">
    <img :src="character.image" alt="character image">
    <h2>{{ character.name }}</h2>
    <p>Статус: {{ character.status }}</p>
    <p>Вид: {{ character.species }}</p>
  </div>
</template>

<script>
export default {
  props: {
    character: Object
  }
}
</script>
