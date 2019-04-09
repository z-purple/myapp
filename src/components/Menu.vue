<template>
  <div class="menu container row mt-5">
    <!-- 左边的菜单展示 -->
    <div class="col-7 text-center">
      <h3 class="text-center text-primary">点餐</h3>
      <table class="table">
        <thead class="bg-primary text-white">
          <tr>
            <th scope="col">尺寸</th>
            <th scope="col">价格(元)</th>
            <th scope="col">加入</th>
          </tr>
        </thead>
        <tbody v-for="(item,index) in items" :key="index">
          <tr>
            <td colspan="3" class="text-danger">{{item.name}}</td> 
          </tr>
          <tr>
            <td colspan="3" class="text-warning">{{item.description}}</td> 
          </tr>
          <tr v-for="(item1,index1) in item.options" :key="index1">
            <td>{{item1.size}}</td>
            <td>{{item1.price}}</td>
            <td>
              <button @click="addToBasket(item,item1)" class="btn btn-success">+</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <!-- 右边的购物车 -->
    <div class="col-5 text-center">
        <h3 class="text-center text-primary">购物车</h3>
        <table class="table">
        <thead class="bg-primary text-white">
          <tr>
            <th scope="col">数量</th>
            <th scope="col">种类</th>
            <th scope="col">价格(元)</th>
          </tr>
        </thead>
        <template v-if="newItems.length>0">
          <tbody v-for="(item,index) in newItems" :key="index">
            <tr>
              <td>
                <button class="btn btn-success btn2" @click="reduce(item,index)">-</button>
                <input type="number" class="input" v-model.number="item.quantity">
                <button class="btn btn-success btn2" @click="add(item)">+</button>
              </td>
              <td>{{item.name}}--{{item.size}}</td>
              <td>{{item.price*item.quantity}}</td>
            </tr>
          </tbody>
          <tr>
              <td></td>
              <td colspan="2" class="text-info">商品总件数:<span class="strong">{{totalNum}}</span></td>
            </tr>
            <tr>
              <td></td>
              <td colspan="2" class="text-info">商品总价格 : <span class="strong">
                 {{totalPrice}}</span></td>
            </tr>
        </template>
        <template v-else>
          <tr>
            <td colspan="3">
              <h3 class="text-danger">此购物车空空如也~</h3>
            </td>
          </tr>
        </template>
      </table>
    </div>
    
  </div>
</template> 

<script>
import axios from 'axios'
export default {
  name: 'Menu',
  data () {
    return {
      items:{},
      // items:{
      //   0:{name:'芝士pizza',description:'这是一款被大众喜爱的Pizza.',options:[{size:'7寸',price:'60'},{size:'10寸',price:'80'}]},
      //   1:{name:'火腿pizza',description:'这是一款女士喜爱的Pizza.',options:[{size:'7寸',price:'50'},{size:'10寸',price:'75'}]},
      // },
      // 表示当我在左边菜单栏添加数据时，newItems才有值。
      newItems:[
        // {quantity:2,name:'火腿pizza-9寸',price:100}
      ]
    }
  },
  mounted(){
    axios.get('./menu-zmf.json')
    .then(res=>{
      // this.items = res.data
      this.$store.commit('setMenuItems',res.data)
    })
  },
  methods:{
    addToBasket(item,options){
      // 点击添加时去重
      // 当前展示的这一项与我们输出的一项吻合时，实现数量quantity+1
      var result = this.newItems.filter((item1)=>{
        return item.name == item1.name && options.size == item1.size
      }) 
      if(result!=null && result.length>0){
        if(result[0].quantity>=10){
          result[0].quantity=10
        }else{
          result[0].quantity++
        }
      }else{ 
        this.newItems.push({
          name:item.name,
          size:options.size,
          quantity:1,
          price:options.price
        })
      }
      
      
    },
    reduce(item,index){
      if(item.quantity>1){
        item.quantity--
      }else{
        this.newItems.splice(index,1)
      }
    },
    add(item){
      if(item.quantity>=10){
        item.quantity=10
      }else{
         item.quantity++
      }
     
    }
  },
  computed:{
    totalNum(){
      return this.newItems.length
    },
    totalPrice(){
      return this.newItems.reduce((sum,cur)=>{
        return sum+cur.quantity*cur.price
      },0)
    },
    items(){
      return this.$store.getters.getMenuItems
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .input{
    width:50px;
    text-align: center;
  }
  .strong{
    font-weight: bolder;
  }
</style>
