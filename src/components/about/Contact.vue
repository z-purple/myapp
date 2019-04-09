<template>
  <div class="contact ">
    <div class="card text-center">
      <div class="card-header">
        联系我们
      </div>
    <div class="card-body">
      <h5 class="card-title">欢迎来到my-pizza</h5>
      <p class="card-text">联系我们这里有各种各样满足你口味的pizza.</p>
      <router-link to="/contact/address" class="btn btn-primary">地址信息</router-link>
      <router-link to="/contact/person" class="btn btn-primary">法人代表</router-link>
      <router-link to="/contact/telphone" class="btn btn-primary">联系方式</router-link>
       <router-view/>
    </div>
    <div class="card-footer text-muted">
      2 days ago
    </div>
  </div>
     
    </div>
</template>

<script>
export default {
  name: 'Contact',
  data () {
    return {
     
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
