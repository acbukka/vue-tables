<template>
  <tr class="table-item">
    <td class="table-item-date table-item__field"> {{ tableItem.id }} </td>
    <td class="table-item-name table-item__field"> {{ tableItem.title }} </td>
    <td class="table-item-count table-item__field"> {{ tableItem.stock }} </td>
    <td class="table-item-distance table-item__field"> {{ tableItem.rating }} </td>
  </tr>
</template>

<script>
export default {
  props: {
    tableItem: {
      type: Object,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
.table-item {
  border-bottom: 1px solid #ddd;
  &__field {
    padding: 3px 0;
  }
  &:nth-of-type(even) {
    background-color: #f3f3f3;
  }
  &:last-of-type {
    border-bottom: 3px solid #009879;
  }
  &__field {
    padding: 10px;
  }
  &:hover {
    color: #009879;
  }
}

</style>