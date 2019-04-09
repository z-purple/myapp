<template>
    <div class="newpizza">
        <h3 class="text-center text-warning">添加新pizza</h3>
        <form>
            <div class="form-group">
                <label for="input1" class="text-warning">品种:</label>
                <input type="text" v-model="newPizza.name" class="form-control" id="input1"  placeholder="请输入您的pizza种类">
            </div>
            <div class="form-group">
                <label class="lable text-warning" for="input2">商品描述:</label>
                <textarea id="input2" v-model="newPizza.description" placeholder="请输入商品的相关描述..." cols="83" rows="2"></textarea>
            </div>
            <h3 class="text-warning">尺寸&价格</h3>
            <div class="form-row">
                <div class="form-group col-md-4">
                    <label for="input3">尺寸:</label>
                    <select id="input3" class="form-control" v-model="newPizza.size1">
                        <option selected>7寸</option>
                        <option>5寸</option>
                        <option>9寸</option>
                        <option>10寸</option>
                        <option>12寸</option>
                    </select>
                </div>
                    <div class="form-group col-md-2">
                    <label for="input4">价格:</label>
                    <input type="text" class="form-control" id="input4" v-model="newPizza.price1">
                </div>
            </div>
            <div class="form-row">
                <div class="form-group col-md-4">
                    <label for="input5">尺寸:</label>
                    <select id="input5" class="form-control" v-model="newPizza.size2">
                        <option selected>7寸</option>
                        <option>5寸</option>
                        <option>9寸</option>
                        <option>10寸</option>
                        <option>12寸</option>
                    </select>
                </div>
                    <div class="form-group col-md-2">
                    <label for="input6">价格:</label>
                    <input type="text" class="form-control" id="input6" v-model="newPizza.price2">
                </div>
            </div>
            <button class="btn btn-primary btn-block" @click.prevent="addPizza">添加pizza</button>
        </form>
    </div>
</template>  

<script>
import axios from 'axios'
export default {
 data () {
    return {
        newPizza: {

        }
    };
 },
 methods: {
     addPizza(){
        var data = {
            name:this.newPizza.name,
            description:this.newPizza.description,
            options:[
                {
                    size:this.newPizza.size1,
                    price:this.newPizza.price1
                },
                {
                    size:this.newPizza.size2,
                    price:this.newPizza.price2
                },
            ]    
        }
        axios.post('./menu-zmf.json',data)
        .then(res=>{
            console.log(res.data) 
            this.$store.commit('pushMenuItems',data)

            // this.$router.push('/menu')
        })
       
     }
 },
};
</script>
<style scoped>
.lable{
    display: block;
}
</style>
