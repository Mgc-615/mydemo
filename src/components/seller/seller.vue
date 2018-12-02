<template>
<div class="seller">
    <div class="toubu">
							<div class="toubutop">
								<p>{{seller.name}}</p>
								<span v-html="xin(seller.deliveryPrice)"></span><span>({{seller.ratingCount}})</span><span>月售{{seller.sellCount}}单</span>
								<div v-html="hxin" class="hongxin" ></div>
								<div class="shouc">
									<span @click="change" v-show="flag">收藏</span>
								</div>
								<div class="shouc"><span @click="changef" v-show="!flag">已收藏</span></div>
							</div>
							<div class="toububott">
								<div class="bott1">
									<span>
										起送价
									</span>
									<p>
										<span>
									  	{{seller.minPrice}}
										</span>元
									</p>
								</div>
								<div class="clear1">
								</div>
								<div class="bott1">
									<span>
										商家配送
									</span>
									<p>
										<span>
											{{seller.deliveryPrice}}
										</span>元
									</p>
								</div>
								<div class="clear1">
								</div>
								<div class="bott1">
									<span>
										平均配送时间
									</span>
									<p>
										<span>
											{{seller.deliveryTime}}
										</span>分钟
									</p>
								</div>
							</div>
						<div class="clear"></div>
						<div class="dibu" v-if="seller.supports">
							<p>公告与活动</p>
							<div id="dibu1">
								{{seller.bulletin}}
							</div>
							<div class="dibu2" v-for="(item,i) in seller.supports" :key="i">
								{{item.description}}
							</div>
						</div>
						<div class="clear"></div>
						<div class="sjsj dibu">
							<p>商家实景</p>
							<div class="sjimg" >
								<div class="sjimg1">
									<img v-for="(pic,i) in seller.pics" :src="pic" :key="i" width="120" height="90" />
								</div>
							</div>
						</div>
						<div class="clear"></div>
						<div class="sjxx dibu">
							<p>商家信息</p>
							<div class="sjxxmain">
								<div class="sjxxs" v-for="(item,i) in seller.infos" :key="i" >
									{{item}}
								</div>
							</div>
						</div>
	</div> 
</div>
</template>

<script>
export default {
  name: "seller",
  props: ["seller"],
  data() {
    return {
	  flag: true,
	  hxin:"<img width='20px' class='xxs' src='./static/img/huix.png'/>",
	  ddd:"change"
    };
  },
  methods: {
    xin(num) {
      var str = "";
      var fnum = Math.floor(num);
      for (var i = 0; i < fnum; i++) {
        str += "<img width='20px'  src='./static/img/xing.png'/>";
      }
      if (num < 5) {
        for (var j = 0; j < 5 - fnum; j++) {
          str += "<img width='20px' class='xxs' src='./static/img/xing1.png'/>";
        }
      }
      return str;
    },
    change() {
	  this.flag = false;
	  this.hxin="<img width='20px' class='xxs' src='./static/img/hongx.png'/>";
    },
    changef() {
	  this.flag = true;
	  this.hxin="<img width='20px' class='xxs' src='./static/img/huix.png'/>";
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.seller{
	overflow-x: hidden;
	margin-top: 175px;
}
.toubutop {
  border-bottom: 1px solid #eee;
  width: 90%;
  margin-left: 5%;
  height: 60px;
  position: relative;
}
.shouc {
  position: absolute;
  right: 0px;
  top: 30px;
  text-align: center;
}
.toubutop p {
  height: 10px;
  margin: 20px 0px;
}
.toubutop span {
  font-size: 12px;
  color: #666;
  margin-right: 10px;
}
.toubutop img {
  width: 20px;
  height: 20px;
}
.toububott {
  display: flex;
}
.toububott .clear1 {
  width: 1px;
  background-color: #eee;
  height: 45px;
  margin-top: 20px;
}
.hongxin{
	width: 20px;
	height: 20px;
	position: absolute;
	right: 10px;
  	top: 10px;

}
.bott1 {
  width: 30%;
  margin-left: 10px;
  margin-top: 20px;
  font-size: 12px;
  text-align: center;
}
.bott1 span {
  font-size: 12px;
  color: #999;
}
.bott1 p {
  height: 0px;
  margin-top: 0;
}
.bott1 p span {
  font-size: 25px;
  color: #333;
}
.dibu {
  width: 90%;
  margin-left: 5%;
}
.dibu p {
  height: 5px;
  margin-top: 20px;
}
#dibu1 {
  color: #f00;
  height: 120px;
  margin-top: 30px;
  padding-left: 5%;
  line-height: 20px;
  font-size: 14px;
}
.dibu2 {
  height: 50px;
  line-height: 50px;
  border-top: 1px solid #eee;
  padding-left: 5%;
}
.clear {
  width: 100%;
  height: 20px;
  background: #f3f5f7;
  border: 1px solid #c6c6c6;
  margin-top: 20px;
}
.sjimg{
	margin-top: 20px;
	overflow-x: scroll;
	
}
.sjimg::-webkit-scrollbar {display:none}
.sjimg1{
	float: left;
	width: 550px;
	height: 100px;
}
.sjimg1 img{
	margin-right: 10px;
}
.sjxxmain{
	margin-top: 20px;
}
.sjxxs{
	font-size: 11.5px;
	height: 40px;
	line-height: 40px;
	border-top: 1px solid #eee;
	padding-left: 5%;
}
</style>
