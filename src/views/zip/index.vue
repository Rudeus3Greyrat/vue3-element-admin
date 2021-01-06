<template>
  <div class="app-container">
    <el-input v-model="filename" placeholder="Please enter the file name (default file)" style="width:300px;" prefix-icon="el-icon-document" />
    <el-button :loading="downloadLoading" style="margin-bottom:20px;" type="primary" icon="el-icon-document" @click="handleDownload">
      Export Zip
    </el-button>
    <el-table v-loading="listLoading" :data="list" element-loading-text="拼命加载中" border fit highlight-current-row>
      <el-table-column align="center" label="ID" width="95">
        <template #default="scope">
          {{ scope.$index }}
        </template>
      </el-table-column>
      <el-table-column label="Title">
        <template #default="scope">
          {{ scope.row.title }}
        </template>
      </el-table-column>
      <el-table-column label="Author" width="95" align="center">
        <template #default="scope">
          <el-tag>{{ scope.row.author }}</el-tag>
        </template>
      </el-table-column>
      <el-table-column label="Readings" width="115" align="center">
        <template #default="scope">
          {{ scope.row.pageviews }}
        </template>
      </el-table-column>
      <el-table-column align="center" label="Date" width="220">
        <template #default="scope">
          <i class="el-icon-time" />
          <span>{{ scope.row.display_time }}</span>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import { ref } from 'vue'
import { fetchList } from '@/api/article'

export default {
  name: 'ExportZip',
  setup() {
    const list = ref(null)
    const listLoading = ref(true)
    const downloadLoading = ref(false)
    const filename = ref('')
    const fetchData = async() => {
      listLoading.value = true
      const { data } = await fetchList()
      list.value = data.items
      listLoading.value = false
    }
    const handleDownload = () => {
      downloadLoading.value = true
      import('@/vendor/Export2Zip').then(zip => {
        const tHeader = ['Id', 'Title', 'Author', 'Readings', 'Date']
        const filterVal = ['id', 'title', 'author', 'pageviews', 'display_time']
        const data = this.formatJson(filterVal, list.value)
        zip.export_txt_to_zip(tHeader, data, filename.value, filename.value)
        downloadLoading.value = false
      })
    }
    const formatJson = (filterVal, jsonData) => {
      return jsonData.map(v => filterVal.map(j => v[j]))
    }
    fetchData()
    return {
      list,
      listLoading,
      downloadLoading,
      filename,
      fetchData,
      handleDownload,
      formatJson
    }
  }
}
</script>
