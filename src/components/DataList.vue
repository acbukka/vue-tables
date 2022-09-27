<template>
  <table class="table">
    <thead>
      <tr class="table-head__tr">
        <th
          class="table-head__th"
          scope="col"
          v-for="column in columns"
        >
          {{ column }}
        </th>
      </tr>
    </thead>
    <transition name="component-fade" mode="out-in">
      <tbody>
        <transition-group name="item-list" v-if="!isItemsLoading">
          <table-item
            v-for="tableItem in tableItems"
            :tableItem="tableItem"
            :key="tableItem.id"
          />
        </transition-group>
        <div v-else>Идет загрузка...</div>
      </tbody>
    </transition>
  </table>
</template>

<script>
import TableItem from "@/components/TableItem";

export default {
  props: {
    columns: {
      type: Array,
      required: true
    },
    tableItems: {
      type: Array,
      required: true
    },
    isItemsLoading: {
      type: Boolean,
      required: true
    }
  },
  components: {
    TableItem
  },
}
</script>

<style lang="scss" scoped>
.table {
  width: 100%;
  border-collapse: collapse;
  border-radius: 5px 5px 0 0;
  overflow: hidden;
  font-size: 1.5em;
  text-align: left;
  &-head__tr {
    letter-spacing: 1px;
    font-weight: bold;
    background-color: #009879;
    color: #fff;
  }
  &-head__th {
    padding: 10px;
  }
}

.item-list-item {
  display: inline-block;
  margin-right: 10px;
}

.item-list-enter-active,
.item-list-leave-active {
  transition: all 0.4s ease;
}

.item-list-enter-from,
.item-list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

</style>