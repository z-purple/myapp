<template>
  <div class="home text-center">
    <div class="box">
      <div class="bg">
          <h1>欢迎来品尝</h1>
          <h2>这里有各种各样好吃的pizza </h2>
          <button @click="goMenu" class="btn btn-primary">Let's Order.</button>
      </div>
      
    </div>
   
    <!-- 路由式渲染组件 -->
    <h3>快递信息</h3>
    <my-delivery></my-delivery> 
    <h3>历史订单</h3>
  </div>
</template>

<script>
import History from '@/components/about/History'
import Delivery from '@/components/about/Delivery'
export default {
  name: 'Home',
  data () {
    return {
     
    }
  },
  methods:{
    goMenu(){
        this.$router.push('/Menu')
    }
  },
  components:{
    'my-delivery':Delivery,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .box{
    background: url('../assets/pizza.jpg');
    width:100%;
    height:700px;
    padding: 10%
  }
  .bg{
    background: #bbb;
    opacity: 0.8;
    width:600px;
    height:200px;
    margin:150px  auto;
    padding:20px;
    position: relative;
  }
  .btn{
    position: absolute;
    left: 245px;
    top: 135px;
  }

</style>
