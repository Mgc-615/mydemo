<template>
  <div id="app">
    <myheader :seller="seller"></myheader>
    <div class="nav">
      <router-link to="/goods">商品</router-link>
      <router-link to="/ratings">评价</router-link>
      <router-link to="/seller">商家</router-link>
    </div>
    <router-view v-if="goods.length>0" :goods="goods" :seller="seller" :ratings="ratings" />
  </div>
</template>

<script>
import myheader from '@/components/myheader/myheader'
import axios from 'axios'

export default {
  name: 'App',
  data: function () {
    return {
      seller: {},
      goods:[],
      ratings:[]
    }
  },
  components:{
    myheader
  } ,
  created(){
      this.getData()
  },
  methods:{
    getData(){
        let url ='http://localhost:8080/static/data.json';
        axios.get(url).then(res=>{
          this.seller=res.data.seller;
          this.goods=res.data.goods;
          this.ratings=res.data.ratings;
        },err=>{
          console.log("error")
        })
    }
  }
}
</script>

<style scoped>
div#app .nav{
  display: flex; 
  width: 100%;
  height: 40px;
  line-height: 40px;
  text-align: center;
  margin-top: 135px;
  position: fixed;
  top: 0;
  z-index: 100;
  background-color: #fff;
}
#app a{
  flex: 1;
  text-decoration: none;
}
#app a.router-link-active{
  color: red;
  border-bottom: 1.5px solid red
}
</style>
