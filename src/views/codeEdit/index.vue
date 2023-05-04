/* eslint-disable */
<template>
    <div class="container">
        <el-card class="box-card" shadow="hover">
            <div slot="header" class="clearfix">
                <el-button type="primary" icon="el-icon-edit" @click="executeCode">运行代码</el-button>
                <el-button type="danger" icon="el-icon-delete" @click="clearCode">清除</el-button>
                <el-button type="warning" icon="el-icon-document-copy" @click="copyCode">复制</el-button>
                <el-button type="success" icon="el-icon-s-platform">生成程序依赖图</el-button>
                <el-button type="success" icon="el-icon-s-platform">生成控制流图</el-button>
                <el-button type="success" icon="el-icon-s-platform">生成函数调用图</el-button>
                <el-upload class="upload-demo" :accept="'.c,.cpp'" :on-change="handleUploadChange">
                    <el-button slot="trigger" size="small" type="info">
                        上传文件
                    </el-button>
                    <div slot="tip" class="el-upload__tip">
                        只能上传C/C++文件
                    </div>
                </el-upload>

            </div>
            <div class="card-body">
                <el-row :gutter="20">
                    <el-col :xs="24" :sm="12" :span="6">
                        <div class="editor">
                            <codemirror ref="myCm" :value="code" :options="cmOptions" @ready="onCmReady" @focus="onCmFocus"
                                @input="onCmCodeChange">
                            </codemirror>
                        </div>
                    </el-col>
                    <el-col :xs="24" :sm="12" :span="4">
                        <div class="output">
                            <pre>{{ output }}</pre>
                        </div>
                    </el-col>
                </el-row>
            </div>
        </el-card>
    </div>
</template>
  
<script>
import 'codemirror/mode/clike/clike.js'

export default {
    data() {
        return {
            code:
                `#include <iostream>
using namespace std;

int main()
{
   cout << "Hello World";
   return 0;
}`,
            output: '',
            cmOptions: {
                tabSize: 4,
                mode: 'text/x-c++src',
                theme: 'default',
                lineNumbers: true,
                line: true,
            }
        }
    },
    methods: {
        onCmReady(cm) {
            console.log('the editor is readied!', cm)
        },
        onCmFocus(cm) {
            console.log('the editor is focus!', cm)
        },
        onCmCodeChange(newCode) {
            console.log('this is new code', newCode)
            this.code = newCode
        },
        executeCode() {
            // 执行代码逻辑
        },
        clearCode() {
            // 清除代码逻辑
        },
        copyCode() {
            // 复制代码逻辑
        },
        handleUploadChange(file) {
            const suffix = file.name.split('.').pop();
            if (suffix !== 'c' && suffix !== 'cpp') {
                this.$message.error('只能上传C/C++文件');
                return false;
            }
            const reader = new FileReader()
            reader.onload = () => {
                const content = reader.result
                this.codemirror.setValue(content)
            }
            reader.readAsText(file.raw)
        }
    },
    computed: {
        codemirror() {
            return this.$refs.myCm.codemirror
        }
    },
    mounted() {
        this.codemirror.setSize("auto", "398px")
        console.log('this is current codemirror object', this.codemirror)
    }
}
</script>
  
<style scoped>
.container {
    display: flex;
    flex-direction: column;
    padding: 10px;
}


.el-button {
    margin: 5px;
}

.card-body {}

.el-row {
    margin-bottom: 20px;
}

.el-col {
    border-radius: 4px;
    height: 100%;
}

.editor {
    height: 400px;
    border: 1px solid #ccc;
    z-index: 0;
}

.editor:hover {
    box-shadow: 0px 0px 5px 1px rgba(0, 0, 0, 0.2);
}

.output {
    height: 400px;
    background-color: #f5f5f5;
    border: 1px solid #ccc;
}

.output:hover {
    box-shadow: 0px 0px 5px 1px rgba(0, 0, 0, 0.2);
}
</style>
  