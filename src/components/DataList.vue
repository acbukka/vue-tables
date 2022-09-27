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
    <tbody>
      <table-item
        v-for="tableItem in tableItems"
        :tableItem="tableItem"
        :key="tableItem.id"
      />
    </tbody>
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
    }
  },
  data() {
    return {
      // tableItems: [],
      // isPostsLoading: false,
      // page: 0,
      // limit: 10,
      // totalPages: 0,
    }
  },
  components: {
    TableItem
  },
  methods: {

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
</style>