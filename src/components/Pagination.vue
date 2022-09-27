<template>
  <div class="pages__wrapper">
    <button
      class="page"
      v-for="pageNumber in pages"
      :class="{
        'current__page': page === pageNumber
      }"
      :key="pageNumber"
      @click="$emit('updatePage', pageNumber)"
    >
      {{ pageNumber }}
    </button>
  </div>
</template>

<script>
export default {
  props: {
    pages: {
      type: Number,
      required: true
    },
    page: {
      type: Number,
      required: true
    },
  }
}
</script>

<style scoped>
.pages__wrapper {
  display: flex;
  justify-content: center;
  margin: 20px auto;
}
.page + .page {
  margin-left: 7px;
}
.page {
  display: flex;
  align-items: center;
  justify-content: center;
  background: transparent;
  border: 2px solid teal;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  padding: 5px;
  transition: all .3s;
}
.page:hover {
  cursor: pointer;
}
.current__page {
  border: 2px solid #009879;
  background: #009879;
  color: white;
}
@media (max-width: 500px) {
  .page {
    width: 25px;
    height: 25px;
  }
  .pages__wrapper {
    margin: 10px auto;
  }
  .page + .page {
    margin-left: 4px;
  }
}
</style>