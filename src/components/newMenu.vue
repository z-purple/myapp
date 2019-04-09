<template>
    <div class="newmenu text-center ">
        <h3 class="text-warning">菜单管理</h3>
        <table class="table">
            <thead>
                <tr>
                    <th scope="col">序号</th>
                    <th scope="col">品种</th>
                    <th scope="col">删除</th>
                </tr>
            </thead>
            <tbody v-for="(item,index) in items" :key="index">
                <tr>
                    <td>{{index+1}}</td>
                    <td>{{item.name}}</td>
                    <td>
                        <button class="btn btn-danger" @click="delItem(item)">Delet</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    data () {
        return {
            // items:[{name:'111'},{name:'111'},{name:'111'},]
            // items:[]
        }
    },
    methods: {
        delItem(item){
            // console.log('./menu-zmf/'+item.id+'.json')
            axios.delete('./menu-zmf/'+item.id+'.json').then(res=>{
                console.log('删除成功')
                // this.$router.push('/menu')
                this.$store.commit('deleteMenuItems',item)
            })
        }
    },
    mounted(){
       var that = this
        axios.get('./menu-zmf.json')
        .then(res=>{
            console.log(res.data)
            // 在这里需要获取下key值==>存储为id，方便通过id删除当前项
            var menus = []
            for(var key in res.data){
                var item = res.data[key]
                item.id =  key
                // that.items.push(item)
                // 用当前的menu来实现数据管理
                menus.push(res.data[key])
            }
            console.log(menus)
            // 优势在于通过vuex=>store,直接实现了数据的更新
            that.$store.commit('setMenuItems',menus)         
        })
    },
    computed:{
        items(){
            return this.$store.getters.getMenuItems 
        }
    }
};
</script>
<style scoped>
</style>
