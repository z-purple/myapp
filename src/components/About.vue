<template>
  <div class="about container mt-5 row">
    <div class="col-4  ">
      <router-link to="/activity" class=" mb-3 text-center list-group-item list-group-item-action list-group-item-success">热门活动</router-link>
      <router-link to="/contact" class=" mb-3 text-center list-group-item list-group-item-action list-group-item-danger">联系我们</router-link>
      <router-link to="/history" class=" mb-3 text-center list-group-item list-group-item-action list-group-item-warning">历史订单</router-link>
      <router-link to="/delivery" class=" mb-3 text-center list-group-item list-group-item-action list-group-item-info">快递信息</router-link>
  </div>
    <div class="col-8 ">
      <router-view/>
    </div>
    
    
  </div>
</template>

<script>
export default {
  name: 'About',
  data () {
    return {
     
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
