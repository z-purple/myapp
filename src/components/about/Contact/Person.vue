<template>
  <div class="person">
    <h3 class="mt-3">{{people}}</h3>
    
  </div>
</template>

<script>
export default {
  name: 'Person',
  data () {
    return {
      people:'全体员工及老板'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
