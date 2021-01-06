<template>
  <el-table :data="list" border fit highlight-current-row style="width: 100%">
    <el-table-column
      v-loading="loading"
      align="center"
      label="ID"
      width="65"
      element-loading-text="请给我点时间！"
    >
      <template #default="scope">
        <span>{{ scope.row.id }}</span>
      </template>
    </el-table-column>

    <el-table-column width="180px" align="center" label="Date">
      <template #default="scope">
        <span>{{ toParseTime(scope.row.timestamp, "{y}-{m}-{d} {h}:{i}") }}</span>
      </template>
    </el-table-column>

    <el-table-column min-width="300px" label="Title">
      <template #default="{ row }">
        <span>{{ row.title }}</span>
        <el-tag>{{ row.type }}</el-tag>
      </template>
    </el-table-column>

    <el-table-column width="110px" align="center" label="Author">
      <template #default="scope">
        <span>{{ scope.row.author }}</span>
      </template>
    </el-table-column>

    <el-table-column width="120px" label="Importance">
      <template #default="scope">
        <svg-icon
          v-for="n in +scope.row.importance"
          :key="n"
          icon-class="star"
        />
      </template>
    </el-table-column>

    <el-table-column align="center" label="Readings" width="95">
      <template #default="scope">
        <span>{{ scope.row.pageviews }}</span>
      </template>
    </el-table-column>

    <el-table-column class-name="status-col" label="Status" width="110">
      <template #default="{ row }">
        <el-tag :type="toStatusFilter(row.status)">
          {{ row.status }}
        </el-tag>
      </template>
    </el-table-column>
  </el-table>
</template>

<script>
import { fetchList } from '@/api/article'
import { parseTime, statusFilter } from '@/utils'

export default {
  props: {
    type: {
      type: String,
      default: 'CN'
    }
  },
  data() {
    return {
      list: null,
      listQuery: {
        page: 1,
        limit: 5,
        type: this.type,
        sort: '+id'
      },
      loading: false
    }
  },
  created() {
    this.getList()
  },
  methods: {
    toParseTime(val1, val2) {
      return parseTime(val1, val2)
    },
    toStatusFilter(val1) {
      return statusFilter(val1)
    },
    getList() {
      this.loading = true
      this.$emit('create') // for test
      fetchList(this.listQuery).then((response) => {
        this.list = response.data.items
        this.loading = false
      })
    }
  }
}
</script>

