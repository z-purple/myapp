<template>
  <div class="delivery row">
   <div class="card col-4 " v-for="(item,index) in items" :key="index">
      <img class="card-img-top" :src="item.imgSrc" alt="Card image cap">
      <div class="card-body">
        <h4 class="card-title">{{item.title}}</h4>
        <p class="card-text text-success">{{item.text}}</p>
        <button class="btn btn-primary"  @click="alert">快递详情</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Delivery',
  data () {
    return {
     items:[
       {imgSrc:require('../../assets/del-sf.png'),title:'顺丰快递',text:'您的快递信息已发送至河北张家口'},
       {imgSrc:require('../../assets/del-yt.jpg'),title:'圆通快递',text:'您的快递信息已发送至山东青岛'},
       {imgSrc:require('../../assets/del-zt.jpg'),title:'中通快递',text:'您的快递信息已发送至洛阳汝阳'}
     ]
    }
  },
  methods:{
    alert(){
      alert('当前快递小哥正在快马加鞭为您派送。')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  img{
    width:100%;
    height:50%;
  }
</style>
