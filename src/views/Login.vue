<template>
    <div class="login">
        <el-card class="yb-login-card">
            <div slot='header'>管理员登录</div>
            <div>
                <el-form label-width="100px">
                    <el-form-item label="管理员名:">
                        <el-input placeholder="请输入管理员名" v-model="formData.aname"></el-input>
                    </el-form-item>

                    <el-form-item label="登录密码:">
                        <el-input placeholder="请输入管理员密码" type='password' v-model="formData.apwd"></el-input>
                    </el-form-item>

                    <el-form-item >
                        <el-button type="primary" @click="doLogin">登录</el-button>
                        <el-button @click="doCancel">取消</el-button>
                    </el-form-item>
                </el-form>
            </div>
        </el-card>
    </div>
</template>

<script>
    export default {
        data(){  //普通组件的模型数据是函数返回值
            return {
                formData:{  //表单中用户输入的两个数据
                    aname:'ding',
                    apwd:'123456'
                }
            }
        },
        methods: {
            doLogin(){  //执行登录
                var url=this.$store.state.globalSettings.apiUrl+`/admin/login/${this.formData.aname}/${this.formData.apwd}`;
                console.log(url)
                this.$axios.get(url).then((res)=>{
                    //console.log(res.data)
                    if(res.data.code==200){
                        //把用户名存入Vuex存储仓库
                        this.$store.commit('setAdminName',this.formData.aname);
                        //执行视图跳转
                        this.$router.push('/main')
                    }else{  //登录失败
                        this.$alert('用户名或密码有误！','登录失败',{type:'error'}).then(()=>{

                        }).catch(()=>{

                        })
                    }
                }).catch((err)=>{
                    console.log(err)
                })
            },
            doCancel(){ //清除用户的输入
                this.formData.aname='';
                this.formData.apwd='';
            }
        }
    }
</script>

<style lang="scss">
    .yb-login-card{
        width:450px;
        margin:100px auto;

        .el-card__header{
            text-align:center;
            font-size:1.2em;
        }
    }
    
</style>