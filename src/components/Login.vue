<template>
  <div class="login">
    <div class="login container text-center mt-3">
    <img src="../assets/logo.png" width="100"  alt="">
    <h3>登陆</h3>
    <form>
      <div class="form-group">
        <input type="email" class="form-control" id="input1"  v-model="username" placeholder="请输入您的账号">
      </div>
      <div class="form-group">
        <input type="password" class="form-control" id="input2" v-model="password" placeholder="请输入您的密码">
      </div>
      <button type="submit"  @click.prevent="onSubmit()" class="btn btn-primary btn-block mt-3">Login</button>
    </form>
  </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Login',
  data () {
    return {
     username:'',
     password:''
    }
  },
  methods:{
    onSubmit(){
      axios.get('./user-zmf.json')
      .then((res)=>{
        console.log(res.data)
        var result = []
        // 用for-in形式来解决对象循环
        for(var key in res.data){
          var user = res.data[key]
          result.push(user)
        }
        console.log(result)
        // 匹配当前的账号密码
        // 1.匹配成功，登陆成功
        // 2.匹配失败，报出账号或密码错误的提醒
        var trueUser = result.filter((user)=>{
          return user.username === this.username && user.password === this.password
        })
        // 如果1.匹配成功，登陆成功
        if(trueUser!=null && trueUser.length>0){
          alert('登陆成功')
          // 发生一个事件到store.js文件
          // currentUser==>赋值
          // isLogin ==>true 
          this.$store.dispatch('setUser',trueUser[0].username)
          sessionStorage.setItem('user',trueUser[0].username)
          this.$router.push('/admin')
        }else{
          alert('登录失败，账号或密码错误')
          // 发送一个事件到store.js文件
          // currentUser==>null
          // isLogin ==>flase
          this.$store.dispatch('setUser',null)
        }
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .form-control{
    width:500px;
  }
  .login{
    width:500px;
    margin: 0 auto;
  }
  .btn{
    width: 107%;
  }
</style>
