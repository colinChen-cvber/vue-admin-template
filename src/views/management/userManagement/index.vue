<template>
    <div class="user-management-container">
        <h2>用户管理</h2>
        <el-form :model="form" label-position="top">
            <el-form-item label="用户名">
                <el-input v-model="form.username"></el-input>
            </el-form-item>
            <el-form-item label="描述">
                <el-input v-model="form.description"></el-input>
            </el-form-item>
            <el-form-item label="权限管理">
                <el-checkbox-group v-model="form.permissions">
                    <el-checkbox label="创建"></el-checkbox>
                    <el-checkbox label="编辑"></el-checkbox>
                    <el-checkbox label="删除"></el-checkbox>
                </el-checkbox-group>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" @click="saveUser">保存</el-button>
            </el-form-item>
        </el-form>
    </div>
</template>
<script>
export default {
    data() {
        return {
            form: {
                username: '',
                description: '',
                permissions: []
            }
        }
    },
    methods: {
        saveUser() {
            // 发送保存用户的请求
            console.log('saving user...')
        }
    }
}
</script>
<style>
.user-management-container {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
}
</style>