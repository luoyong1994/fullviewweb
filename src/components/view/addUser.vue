<template>
  <div class="header">
    <el-form :label-position="position" label-width="100px" :model="formLabelAlign" :rules="rules" ref="formLabelAlign" class="demo-ruleForm">
      <el-form-item label="用户名" prop="userName">
        <el-input v-model="formLabelAlign.userName"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="userPassword">
        <el-input v-model="formLabelAlign.userPassword"></el-input>
      </el-form-item>
      <el-form-item label="电话" prop="userPhone">
        <el-input v-model="formLabelAlign.userPhone"></el-input>
      </el-form-item>
      <el-form-item label="人员类型" prop="userType" size="medium">
        <el-radio-group v-model="formLabelAlign.userType">
          <el-radio label="1">管理员</el-radio>
          <el-radio label="0">校内用户</el-radio>
        </el-radio-group>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm('formLabelAlign')">立即创建</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
/* eslint-disable */
import { addAdmin } from '@/api/api'
export default {
    name: '',
    props: [''],
    data() {
        return {
            position: 'left',
            formLabelAlign: {
                userName: '',
                userPassword: '',
                userPhone: '',
                userType: ''
            },
            rules: {
                userName: [
                    { required: true, message: '请输入用户名', trigger: 'blur' }
                ],
                userPassword: [
                    { required: true, message: '请输入密码', trigger: 'blur' }
                ],
                userPhone: [
                    {
                        required: true,
                        message: '请输入电话号码',
                        trigger: 'blur'
                    }
                ],
                userType: [
                    {
                        required: true,
                        message: '请选择人员类型',
                        trigger: 'change'
                    }
                ]
            }
        }
    },

    components: {},

    computed: {},

    beforeMount() {},

    mounted() {},

    methods: {
        submitForm(formName) {
            this.$refs[formName].validate(valid => {
                console.log(this.formLabelAlign)
                if (valid) {
                    addAdmin(this.formLabelAlign).then(res => {
                        if (res.state == 0) {
                            this.$message({
                                message: '添加成功！',
                                type: 'success'
                            })
                            var userType = this.formLabelAlign.userType
                            if (userType == 0) {
                                this.$router.push({ name: 'readerPage' })
                            } else {
                                this.$router.push({ name: 'adminPage' })
                            }
                        }
                    })
                } else {
                    return false
                }
            })
        }
    },

    watch: {}
}
</script>
<style scoped>
.header{
  width: 600px;
  margin: 10px auto;
}
</style>