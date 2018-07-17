<template>
  <div class="login"> 
    <el-form ref="form" :model="form" class="container" :rules="rules" >
      <div class="login-img">
      </div>
  <el-form-item prop="username">
    <el-input v-model="form.username" placeholder="账户"  prefix-icon="myicon myicon-user" ></el-input>
  </el-form-item>
  <el-form-item prop="password">
    <el-input v-model="form.password" placeholder="密码"  type='password' prefix-icon="myicon myicon-key" ></el-input>
  </el-form-item>
  <el-form-item>
      <el-button type="primary" class="login-btn" @click="loginSubmit('form')">登录</el-button>
  </el-form-item>
    </el-form>
  </div>
</template>
<script>
import {checkUser} from '@/api';
  export default{
    data(){
      return{
        form:{
          username:'',
          password:''
        },
        rules:{
          username:[
          { required: true, message: '请输入正确的账号', trigger: 'blur' } 
          ],
          password:[
          { required: true, message: '请输入正确的密码', trigger: 'blur' } 
        ]
       }
      }
    },
    methods:{
      loginSubmit(formName){
        this.$refs[formName].validate(valide=>{
          //只有校验通过才执行函数
          if(valide){
           checkUser(this.form).then(res=>{
             //如果成功需要跳转
             if(res.meta.status===200){
               this.$router.push({name:"Home"})
              //  console.log('登录成功')
             }else{
               this.$message({
                 type:'error',
                 message:res.meta.msg
               })
             }
             //如果事变,展示提示信息
           })
          }else{
            console.log('校验不通过')
          }
        })
      }

      
    }
  }
</script>
<style lang="scss" scoped>
.login{
  position:fixed;
  width:100%;
  height:100%;
  background-color: #2f4050;
  .container{
    width: 550px;
    height: 300px;
    margin:200px auto;
    padding:40px;
    padding-top: 90px;
    border: 1px solid #ccc;
    box-sizing: border-box;
    position: relative;
    }
      .login-img{
         width: 120px;
         height: 120px;
         border-radius: 50%;
         background:url(../assets/avatar.jpg);
         position: absolute;
         left: 50%;
         transform: translateX(-50%);
         top:-75px;
         border: 10px solid #fff;
         box-shadow: 1px 1px 1px #ccc;

  }
  .login-btn{
    width: 100%;
  }
}

</style>
