<template>
  <div class="admin container row mt-3">
    <!-- 添加新的pizza -->
    <div class="col-7">
      <NewPizza></NewPizza>
    </div>
    <!-- 菜单管理 -->
    <div class="col-5">
      <NewMenu></NewMenu>
    </div>
  </div>
</template>

<script>
import NewPizza from '@/components/NewPizza'
import NewMenu from '@/components/NewMenu'
export default {
  name: 'Admin',
  data () {
    return {
     
    }
  },
  components:{
    'NewPizza':NewPizza,
    'NewMenu':NewMenu
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
