<template>
  <div>
    <div class="filter-form">
      <input v-model="nameFilter" placeholder="Фильтровать по названию">
      <select v-model="statusFilter">
        <option value="">Все</option>
        <option value="Alive">Живой</option>
        <option value="Dead">Мертвый</option>
        <option value="unknown">Ни жив, ни мёртв</option>
      </select>
      <button @click="applyFilters">Применить</button>
    </div>
    <div class="characters">
      <CharacterCard v-for="character in characters" :key="character.id" :character="character" />
    </div>
    <div class="pagination">
      <PaginationComponent :currentPage="currentPage" :totalPages="totalPages" @page-changed="fetchCharacters"/>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import CharacterCard from './CharacterCard.vue';
import PaginationComponent from './PaginationComponent.vue';

export default {
  name: 'CharacterList',
  components: { CharacterCard, PaginationComponent },
  data() {
    return {
      characters: [],
      nameFilter: '',
      statusFilter: '',
      currentPage: 1,
      totalPages: 1
    };
  },
  methods: {
    async fetchCharacters(page = 1) {
      this.currentPage = page;
      const response = await axios.get(`https://rickandmortyapi.com/api/character`, {
        params: {
          page,
          name: this.nameFilter,
          status: this.statusFilter
        }
      });
      this.characters = response.data.results;
      this.totalPages = response.data.info.pages;
    },
    applyFilters() {
      this.fetchCharacters(1);
    }
  },
  created() {
    this.fetchCharacters();
  }
}
</script>

