<template>
  <div class="goods">
      <div class="goods-left" ref="goodsleft">
        <ul>
          <li v-for="(item,index) in goods" :key="index" :class="{'current':currentIndex===index}" @click="selectMenu(index)" >
             {{item.name}}
          </li>
        </ul>
      </div>
      <div class="goods-right" ref="goodsright">
        <ul class="right">
          <li v-for="(item,index) in goods" :key="index"  ref="foodList">
             <div class="title">
               {{item.name}}
             </div>
              <div class="sp" v-for="(v,k) in item.foods" :key="k" >
                 <div class="spimg">
                   <img :src="v.icon" width="57"/>
                  </div>
                  <div class="spmain">
                    <div class="foodname">{{v.name}}</div>
                    <div class="description" v-show="v.description">{{v.description}}</div>
                    <div class="sellcount"><span>月售{{v.sellCount}}</span><span>好评率{{v.rating}}</span></div>
                    <div class="price">￥{{v.price}}</div>
                  </div>
                  <div class="caradd">
                    <addjian :food="v"></addjian>
                  </div>
                  
              </div>
          </li>
        </ul>
      </div>
      <div class="shopcar">
         <shopcar :goods='goods'> </shopcar>
      </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
import addjian from '@/components/addjian/addjian'
import shopcar from '@/components/shopcar/shopcar'
// let wrapper = document.querySelector('.goods-right')
// let scroll = new BScroll(wrapper)
// scroll.scrollToElement(wrapper, 10, false, true, easing)
export default {
  name: 'goods',
  props:["goods"],
  data () {
    return {
       listHeight: [],
       scrollY: 0,
       food:'',
       foods:[],
    }
  },
   components:{
    addjian,
    shopcar
  },
  computed:{
    currentIndex () {
      // console.log("listHeight.length:",this.listHeight);
        for (let i = 0; i < this.listHeight.length; i++) {
          let height1 = this.listHeight[i];
          let height2 = this.listHeight[i + 1];
          // this:VueComponent
          // console.log('goods页面,this:', this)
          if (!height2 || (this.scrollY >= height1 && this.scrollY < height2)) {
            if(i>= this.listHeight.length/2){
              let elMenu =this.$refs.goodsleft.children[0].children[this.listHeight.length/2];
              this.meunScroll.scrollToElement(elMenu,300)
            }else{
              let elMenu2=this.$refs.goodsleft.children[0].children[0]
              this.meunScroll.scrollToElement(elMenu2,300)
            }
            return i;
          }
        }
        return 0;
    }
  },
  mounted() {
    this.initScroll();
    this.calculateHeight();
  },
  methods:{
    selectMenu (index) {
        let foodList = this.$refs.foodList;
        let el = foodList[index];
        this.foodsScroll.scrollToElement(el, 300)
      },
       initScroll () {
        this.meunScroll = new BScroll(this.$refs.goodsleft, {
          click: true
        })

        this.foodsScroll = new BScroll(this.$refs.goodsright, {
          click: true,
          probeType: 3
        })

        // 滚动方法
        this.foodsScroll.on('scroll', (pos) => {
          this.scrollY = Math.abs(Math.round(pos.y))
        })
      },
      calculateHeight () {
        let foodList = this.$refs.foodList;
        //vue里面的传过来的的goods不加v-if 判断不为空时 就会获取不到foodList的长度
        // console.log("foodList:",foodList)
        let height = 0;
        this.listHeight.push(height);
        for (let i = 0; i < foodList.length; i++) {
          let item = foodList[i];
          height += item.clientHeight;
          this.listHeight.push(height)
        }
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  div.goods{
    width: 100%;
    display: flex;
    overflow: hidden;
    position: absolute;
    top: 175px;
    bottom: 0px;
  }
  .goods-left{
    width: 25%;
    background: #eee;    
  }
  .current{
    background: #fff;
    font-weight: 700;
  }
  .goods-right{
    flex: 1;
  }
  .goods-left ul li{
    height: 30px;
    padding: 20px 10px;
    color: #666;
    text-align: center;
  }

 .goods-right ul li .sp{
   display: flex;
   position: relative;
   padding: 20px 20px;
 }
 .title{
   width: 100%;
   height: 30px;
   line-height: 30px;
   font-size: 13px;
   padding-left: 20px;
   background-color: #eee;
   border-left: 2px solid #bbb;
   color: #333;
 }
 .spmain{
   margin-left: 10px;
 }
 .foodname{
   height: 20px;
   line-height: 20px;
   font-size: 15px;
 }
 .description{
    height: 20px;
   line-height: 20px;
   font-size: 11px;
   color: #999;
 }
 .sellcount{
    height: 20px;
   line-height: 20px;
   font-size: 11px;
   color: #999;
 }
 .sellcount span{
   margin-right: 10px;
 }
 .price{
   color: #f00;
   font-size: 14px;
 }
 .caradd{
   position: absolute;
   right: 0px;
  bottom: 30px;
 }
 .shopcar{
   width: 100%;
   height: 60px;
   background: #000;
  position: absolute;
  bottom: -5px;
 }
</style>
