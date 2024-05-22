<template>
  <div>
    <button @click="changePage(currentPage - 1)" :disabled="currentPage === 1">Предыдущая страница</button>
    <span>Страница {{ currentPage }} из {{ totalPages }}</span>
    <button @click="changePage(currentPage + 1)" :disabled="currentPage === totalPages">Следующая страница</button>
  </div>
</template>

<script>
export default {
  name: 'PaginationComponent',
  props: {
    currentPage: Number,
    totalPages: Number
  },
  methods: {
    changePage(page) {
      this.$emit('page-changed', page);
    }
  }
}
</script>
