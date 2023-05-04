<template>
    <div class="model-container">
        <h2>模型管理</h2>
        <el-form :model="form" label-position="top">
            <el-form-item label="数据集">
                <el-input v-model="form.dataset"></el-input>
            </el-form-item>
            <el-form-item label="模型名称">
                <el-input v-model="form.modelName"></el-input>
            </el-form-item>
            <el-form-item label="训练集测试集比例">
                <el-slider v-model="form.trainTestRatio" :min="0" :max="1" :step="0.1"></el-slider>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" @click="trainModel">训练</el-button>
            </el-form-item>
        </el-form>
    </div>
</template>
<script>
export default {
    data() {
        return {
            form: {
                dataset: '',
                modelName: '',
                trainTestRatio: 0.8
            }
        }
    },
    methods: {
        trainModel() {
            // 发送训练模型的请求
            console.log('training model...')
        }
    }
}
</script>
<style>
.model-container {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
}
</style>