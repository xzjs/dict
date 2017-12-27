<template>
    <div>
        <el-container>
            <el-header>
                <el-input placeholder="请输入内容" v-model="keyword" class="input-with-select" clearable>
                    <el-button slot="append" icon="el-icon-search" @click="search"></el-button>
                </el-input>
            </el-header>
            <el-main>
                <div v-for="item in datas" class="word">
                    {{item.word}}
                </div>
            </el-main>
        </el-container>
    </div>
</template>

<script>
    import axios from 'axios';

    axios.defaults.baseURL = "http://website.xzjs.love";

    export default {
        name: 'HelloWorld',
        data() {
            return {
                keyword: '',
                datas: []
            }
        },
        methods: {
            search() {
                var vm = this;
                axios.get('/dicts', {
                    params: {
                        keyword: this.keyword
                    }
                }).then(function (response) {
                    if (response.data.status == true) {
                        vm.datas = response.data.data;
                    } else {
                        console.log(response.data.data);
                    }
                }).catch(function (error) {
                    console.log(error)
                })
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .el-header {
        background-color: #B3C0D1;
        color: #333;
        text-align: center;
        line-height: 60px;
    }

    .el-main {
        background-color: #E9EEF3;
        color: #333;
        text-align: center;
    }

    body > .el-container {
        margin-bottom: 40px;
    }

    .input-with-select .el-input-group__prepend {
        background-color: #fff;
    }

    .el-container .el-main .word {
        display: inline;
        float: left;
        width: 100px;
    }
</style>
