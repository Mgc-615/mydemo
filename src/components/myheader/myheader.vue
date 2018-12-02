<template>
<div class="sss">
  <div class="myheader">
    <div class="hmsg" @click="open">
       <div class="himg"><img :src="seller.avatar" width="64" height="64"></div>
       <div class="hmain">
          <div class="title"><span>品牌</span>{{seller.name}}</div>
          <div class="description" >{{seller.description}}/{{seller.deliveryTime}}分钟送达</div>
          <div class="support" v-if="seller.supports"><span>满</span>{{seller.supports[0].description}}</div>
        </div>
    </div>
    <div class="sjxx" v-if="seller.supports"  @click="open"><span>{{seller.supports.length}}个></span></div>
    <div class="gonggao" @click="open"><span>{{seller.bulletin}}</span></div>
    <div class="backimg"><img :src="seller.avatar" ></div>
    <div class="tanchuan" v-show="flag">
        <p>{{seller.name}}</p>
        <div class="xing" v-html="xin(seller.score)" ></div>
        <div class="yhmsg"><span>———————</span>优惠信息<span>———————</span></div>
        <div class="yhmain" v-if="seller.supports" >
          <div v-for="(item,i) in seller.supports" :key="i" >{{item.description}}</div>
        </div>
        <div class="yhmsg"><span>———————</span>商家公告<span>———————</span></div>
        <div class="sjgg">
            <div class="sjmain">
              {{seller.bulletin}}
            </div>
        </div>
        <div class="close" @click="close">x</div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'myheader',
  data () {
    return {
      flag:false
    }
  },
  props:["seller"],
  methods:{
    	 xin(num){
					var str ="";
					var fnum =Math.floor(num)
				for(var i=0;i<fnum;i++){
					str+="<img width='25px'  src='./static/img/xing.png'/>"
				}
				if(num<5){
						for(var j=0;j<5-fnum;j++){
						str+="<img width='25px' class='xxs' src='./static/img/xing1.png'/>";
					}
				}
				return str
      },
      close(){
          this.flag=false;
      },
      open(){
          this.flag=true;
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    div.sss{
      position: fixed;
      top: 0;
       width: 100%;
      height: 134px;
      z-index: 1000;
      background-color:rgba(0,0,0,0.8)
    }  
    div.myheader{
      width: 100%;
      height: 134px;
      position: relative;
      color: #fff;
      background-color:rgba(0,0,0,0.4)
    }
    div.hmsg{
      display: flex;
      position: absolute;
      top: 20px;
      left: 20px;
    }
    div.hmain{
      margin-left: 10px
    }
    div.title{
      font-weight: 700;
      height: 25px;
      line-height: 25px;
    }
     div.description{
      height: 15px;
      line-height: 15px;
      font-size: 12px;
    }
    div.support{
      height: 25px;
      line-height: 25px;
      font-size: 10px
    }
    div.gonggao{
      width: 100%;
      background-color:rgba(7,17,27,0.4);
      height: 25px;
      line-height: 25px;
      font-size: 10px;
      overflow-x: hidden;
      white-space: nowrap;
      text-overflow: ellipsis;
      position: absolute;
      bottom: 0;
    }
    div.sjxx{
      width: 35px;
      height: 20px;
      line-height: 20px;
      font-size: 10px;
      text-align: center;
      background-color:rgba(0,10,0,0.4);
      border-radius: 10px;
      position: absolute;
      right: 10px;
      bottom: 50px;
    }
    div.backimg{
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: -1;
      -webkit-filter: blur(10px);
      filter: blur(10px);
    }
    div.backimg img{
      width: 100%;
      height: 134px;
    }
    div.tanchuan{
      position: fixed;
      z-index: 15000;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      overflow: auto;
      -webkit-backdrop-filter: blur(10px);
      backdrop-filter: blur(10px);
      opacity: 1;
      background: rgba(7,17,27,0.8);
      text-align: center;
    }
    div.tanchuan p{
      font-weight: 700;
      font-size: 18px;
      margin-top: 60px;
    }
    div.tanchuan .yhmsg{
      font-weight: 700;
      font-size: 16px;
      margin-top: 30px;
    }
    div.tanchuan .yhmsg span{
      color: #4C535A;
      display: inline-block;
      font-weight: 700;
      margin: 0px 10px;
    }
    div.yhmain{
      text-align: left;
      margin-left: 50px;
    }
     div.yhmain div{
       margin-top: 15px;
       font-size: 14px;
     }
     div.sjgg{
       margin-top: 20px;
        text-align: left;
        margin-left: 50px;
     }
     div.sjgg .sjmain{
       font-size: 14px;
       line-height: 25px;
     }
     div.xing{
       margin-top: 20px;
     }
     div.close{
       width: 30px;
       height: 30px;
       font-size: 30px;
       font-weight: 700;
       cursor: pointer;
       position: fixed;
       bottom: 80px;
       left: 50%;
     }
</style>
