<template>
  <div class="app">
    <div class="app__inner">
      <div class="data-params">
        <div class="column-select">
          <my-select
            v-model="selectedColumn"
            :options="options.columns"
          >
            Поиск по:
          </my-select>
        </div>
        <div class="condition__select">
          <my-select
            v-model="selectedCondition"
            :options="options.conditions"
          >
            Условие:
          </my-select>
          <my-input
            v-model="searchQuery"
          >
            Значение:
          </my-input>
        </div>
      </div>
      <data-list
        :columns="options.columns"
        :tableItems="filteredItems"
      />
    </div>
  </div>
</template>

<script>
import DataList from "@/components/DataList";
import MySelect from "@/components/UI/MySelect";
import axios from "axios";

export default {
  name: 'App',
  components: {
    MySelect,
    DataList
  },
  data() {
    return {
      tableItems: [],
      isItemsLoading: false,
      page: 0,
      limit: 10,
      totalPages: 0,
      selectedColumn: 'Дата',
      selectedCondition: 'Содержит',
      searchQuery: '',
      options: {
        columns: ['Дата', 'Название', 'Количество', 'Расстояние'],
        conditions: ['Содержит', 'Равно', 'Больше', 'Меньше']
      }
    }
  },
  computed: {
    filteredItems() {
      switch (this.selectedCondition) {
        case 'Содержит':
          switch (this.selectedColumn) {
            case 'Дата':
              return this.filteredText('id');
            case 'Название':
              return this.filteredText('title');
            case 'Количество':
              return this.filteredText('stock');
            case 'Расстояние':
              return this.filteredText('rating');
          }
          break;
        case 'Равно':
          switch (this.selectedColumn) {
            case 'Дата':
              return this.filterNumbers('Равно', 'id')
            case 'Название':
              return this.filteredText('title')
            case 'Количество':
              return this.filterNumbers('Равно', 'stock')
            case 'Расстояние':
              return this.filterNumbers('Равно', 'rating')
          }
          break
        case 'Больше':
          switch (this.selectedColumn) {
            case 'Дата':
              return this.filterNumbers('Больше', 'id')
            case 'Название':
              return this.filteredText('title')
            case 'Количество':
              return this.filterNumbers('Больше', 'stock')
            case 'Расстояние':
              return this.filterNumbers('Больше', 'rating')
          }
          break
        case 'Меньше':
          switch (this.selectedColumn) {
            case 'Дата':
              return this.filterNumbers('Меньше', 'id')
            case 'Название':
              return this.includeFilter('title')
            case 'Количество':
              return this.filterNumbers('Меньше', 'stock')
            case 'Расстояние':
              return this.filterNumbers('Меньше', 'rating')
          }
          break
      }
    },
  },
  methods: {
    filteredText(column) {
      return this.includeFilter(column)
    },
    filterNumbers(condition, column) {
      switch (condition) {
        case 'Равно':
          if (this.searchQuery) {
            return this.tableItems.filter(item => item[column] === Number(this.searchQuery))
          } else {
            return this.tableItems.filter(item => item);
          }
        case 'Больше':
          if (this.searchQuery) {
            return this.tableItems.filter(item => item[column] > Number(this.searchQuery))
          } else {
            return this.tableItems.filter(item => item);
          }
        case 'Маньше':
          if (this.searchQuery) {
            return this.tableItems.filter(item => item[column] < Number(this.searchQuery))
          } else {
            return this.tableItems.filter(item => item);
          }
      }
    },
    includeFilter(column) {
      if (this.searchQuery) {
        return this.tableItems.filter(item => String(item[column]).toLowerCase().includes(this.searchQuery.toLowerCase()))
      } else {
        return this.tableItems.filter(item => item);
      }
    },
    async fetchItems () {
      try {
        const response = await axios.get('https://dummyjson.com/products', {
          params: {
            skip: this.page * 10,
            limit: this.limit
          }
        });
        this.tableItems = response.data.products;
        this.totalPages = response.data.total / 10;
      } catch (err) {
        alert('Ошибка');
      } finally {

      }
    },
  },
  mounted() {
    this.fetchItems()
  },
}
</script>

<style lang="scss">

.app {
  font-family: 'Nunito', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  padding: 0 20px;
  &__inner {
    margin: 0 auto;
    width: 800px;
  }
}

.data-params {
  margin: 50px 0;
}

.condition__select {
  display: flex;
}

</style>
