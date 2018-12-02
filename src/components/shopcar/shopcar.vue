<template>
  <div class="shopcar">
   件数:{{allcount}} 总价：{{allprice}}
  </div>
</template>

<script>
 import vue from 'vue'
export default {
  props:["goods"],
  data () {
    return {
       price:0,
       counts:0,
       foods:[]
    }
  },
  methods:{
  },
  computed:{
    allcount(){
      this.counts=0;
      for(let i=0;i< this.goods.length;i++){
        for(let j=0;j< this.goods[i].foods.length;j++){
          if(this.goods[i].foods[j].count){
            this.counts+=this.goods[i].foods[j].count;
          }else{
            return this.counts
          }
        }
      }
    },
    allprice(){
      this.price=0;
      for(let i in this.goods){
        for(let j in this.goods[i].foods){
          if(!this.goods[i].foods[j].count){
            return this.price
          }else{
            this.price+=this.goods[i].foods[j].count*this.goods[i].foods[j].price;
          }
        }
      }
      return this.price
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.shopcar{
  color: #fff;
}
</style>
