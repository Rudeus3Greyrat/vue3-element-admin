<template>
  <el-dropdown :show-timeout="100" trigger="click">
    <el-button plain>
      {{ !comment_disabled ? "Comment: opened" : "Comment: closed" }}
      <i class="el-icon-caret-bottom el-icon--right" />
    </el-button>
    <template #dropdown>
      <el-dropdown-menu class="no-padding">
        <el-dropdown-item>
          <el-radio-group v-model="comment_disabled" style="padding: 10px">
            <el-radio :label="true"> Close comment </el-radio>
            <el-radio :label="false"> Open comment </el-radio>
          </el-radio-group>
        </el-dropdown-item>
      </el-dropdown-menu>
    </template>
  </el-dropdown>
</template>

<script>
export default {
  props: {
    value: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    comment_disabled: {
      get() {
        return this.value
      },
      set(val) {
        this.$emit('input', val)
      }
    }
  }
}
</script>
