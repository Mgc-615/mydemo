<template>
  <div class="addjian">
   <span class="jian" v-if="food.count" @click="jian()">-</span>
   <span  v-if="food.count">{{food.count}}</span> 
   <span class="add" @click="add()">+</span>
  </div>
</template>

<script>
 import vue from 'vue'
export default {
  props:["food"],
  data () {
    return {
       
    }
  },
  methods:{
    add(){
      if(this.food.count){
        this.food.count++;
        console.log("food",this.food)
      }else{
        vue.set(this.food, 'count', 1);
        console.log("food",this.food)
      }
    },
    jian(){
        this.food.count--;
    }
  },
  computed:{
  
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.addjian{
  display: flex;
  justify-content: space-around;
  text-align: center;
}
.addjian span{
  margin-right: 10px;
}
.add,.jian{
   width: 20px;
   height: 20px;
   line-height: 20px;
   text-align: center;
   color: #fff;
   font-size: 15px;
   background-color: #00A0DC;
   border-radius: 50%;
 }
</style>
