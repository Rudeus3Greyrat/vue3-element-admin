<template>
  <div class="app-container">
    <el-card class="box-card">
      <template #header>
        <div>
          <a
            class="link-type link-title"
            target="_blank"
            href="https://panjiachen.github.io/vue-element-admin-site/guide/advanced/theme.html"
          >
            Theme documentation
          </a>
        </div>
      </template>
      <div class="box-item">
        <span class="field-label">Change Theme : </span>
        <el-switch v-model="theme" />
        <aside style="margin-top: 15px">
          Tips: It is different from the theme-pick on the navbar is two
          different skinning methods, each with different application scenarios.
          Refer to the documentation for details.
        </aside>
      </div>
    </el-card>

    <div class="block">
      <el-button type="primary"> Primary </el-button>
      <el-button type="success"> Success </el-button>
      <el-button type="info"> Info </el-button>
      <el-button type="warning"> Warning </el-button>
      <el-button type="danger"> Danger </el-button>
    </div>

    <div class="block">
      <el-button type="primary" icon="el-icon-edit" />
      <el-button type="primary" icon="el-icon-share" />
      <el-button type="primary" icon="el-icon-delete" />
      <el-button type="primary" icon="el-icon-search"> Search </el-button>
      <el-button type="primary">
        Upload
        <i class="el-icon-upload el-icon-right" />
      </el-button>
    </div>

    <div class="block">
      <el-tag
        v-for="tag in tags"
        :key="tag.type"
        :type="tag.type"
        class="tag-item"
      >
        {{ tag.name }}
      </el-tag>
    </div>

    <div class="block">
      <el-radio-group v-model="radio">
        <el-radio :label="3"> Option A </el-radio>
        <el-radio :label="6"> Option B </el-radio>
        <el-radio :label="9"> Option C </el-radio>
      </el-radio-group>
    </div>

    <div class="block">
      <el-slider v-model="slideValue" />
    </div>
  </div>
</template>

<script>
import { ref, watch } from 'vue'
import { toggleClass } from '@/utils'
import '@/assets/custom-theme/index.css' // the theme changed version element-ui css

export default {
  name: 'Theme',
  setup() {
    const theme = ref(false)
    const tags = ref([
      { name: 'Tag One', type: '' },
      { name: 'Tag Two', type: 'info' },
      { name: 'Tag Three', type: 'success' },
      { name: 'Tag Four', type: 'warning' },
      { name: 'Tag Five', type: 'danger' }
    ])
    const slideValue = ref(50)
    const radio = ref(3)
    watch(theme, () => toggleClass(document.body, 'custom-theme'))
    return { theme, tags, slideValue, radio }
  }
}
</script>

<style scoped>
.field-label {
  vertical-align: middle;
}
.box-card {
  width: 400px;
  max-width: 100%;
  margin: 20px auto;
}

.block {
  padding: 30px 24px;
}

.tag-item {
  margin-right: 15px;
}
</style>
