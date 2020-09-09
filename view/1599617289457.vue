<template>
  <div>
    <el-dialog v-bind="$attrs" v-on="$listeners" @open="onOpen" @close="onClose" title="Dialog Titile">
      <el-form ref="elForm" :model="formData" :rules="rules" size="medium" label-width="100px">
        <el-form-item label="手机号" prop="mobile">
          <el-input v-model="formData.mobile" placeholder="请输入手机号" :maxlength="11" show-word-limit clearable
            prefix-icon='el-icon-mobile' :style="{width: '100%'}"></el-input>
        </el-form-item>
        <el-form-item label="单行文本" prop="field101">
          <el-input v-model="formData.field101" placeholder="请输入单行文本" clearable :style="{width: '100%'}">
          </el-input>
        </el-form-item>
        <el-form-item label="计数器" prop="field102">
          <el-input-number v-model="formData.field102" placeholder="计数器"></el-input-number>
        </el-form-item>
        <el-form-item label="开关" prop="field103" required>
          <el-switch v-model="formData.field103"></el-switch>
        </el-form-item>
        <el-row :gutter="15">
          <el-form-item label="多选框组" prop="field110">
            <el-checkbox-group v-model="formData.field110" size="medium">
              <el-checkbox v-for="(item, index) in field110Options" :key="index" :label="item.value"
                :disabled="item.disabled">{{item.label}}</el-checkbox>
            </el-checkbox-group>
          </el-form-item>
        </el-row>
      </el-form>
      <div slot="footer">
        <el-button @click="close">取消</el-button>
        <el-button type="primary" @click="handelConfirm">确定</el-button>
      </div>
    </el-dialog>
  </div>
</template>
<script>
export default {
  inheritAttrs: false,
  components: {},
  props: [],
  data() {
    return {
      formData: {
        mobile: '',
        field101: undefined,
        field102: undefined,
        field103: false,
        field110: [2, 1],
        field111: false,
      },
      rules: {
        mobile: [{
          required: true,
          message: '请输入手机号',
          trigger: 'blur'
        }, {
          pattern: /^1(3|4|5|7|8|9)\d{9}$/,
          message: '手机号格式错误',
          trigger: 'blur'
        }],
        field101: [{
          required: true,
          message: '请输入单行文本',
          trigger: 'blur'
        }],
        field102: [{
          required: true,
          message: '计数器',
          trigger: 'blur'
        }],
        field110: [{
          required: true,
          type: 'array',
          message: '请至少选择一个field110',
          trigger: 'change'
        }],
      },
      field110Options: [{
        "label": "选项一",
        "value": 1
      }, {
        "label": "选项二",
        "value": 2
      }],
    }
  },
  computed: {},
  watch: {},
  created() {},
  mounted() {},
  methods: {
    onOpen() {},
    onClose() {
      this.$refs['elForm'].resetFields()
    },
    close() {
      this.$emit('update:visible', false)
    },
    handelConfirm() {
      this.$refs['elForm'].validate(valid => {
        if (!valid) return
        this.close()
      })
    },
  }
}

</script>
<style>
</style>
