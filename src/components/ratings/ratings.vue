<template>
  <div class="ratings">
    <div class="pfen">
								<div class="pfenleft">
									<span>{{seller.score}}</span>
									<p>综合评分</p>
									<span>高于周边商家{{seller.rankRate}}%</span>
								</div>
							<div class="pfenright">
								<div class="xing">
									<span>服务态度</span>
									<div v-html="xin(seller.serviceScore)"></div>
									<span>4.1</span>
								</div>
								<div class="xing">
									<span>商品评分</span>
									<div v-html="xin(seller.foodScore)"></div>
									<span>4.3</span>
								</div>
								<div id="songd">
									<span>送达时间</span>
									<span>38分钟</span>
								</div>
							</div>
		 </div>
     <div class="clear"></div>
     <div class="pingjia">
       <div class="ratingselect">
         <div class="rating-type" >
           <span :class="raclass" @click="change(ratings)" >全部<span class="count">24</span></span>
            <span :class="manclass" @click="change1(ratings)">满意<span class="count">18</span></span> 
            <span :class="buclass" @click="change2(ratings)">不满意<span class="count">6</span></span></div> 
         <div class="switch" @click="gouc(ratings)">
           <span class="icon" v-show="gou"></span> 
           <span class="icon icon1" v-show="!gou"></span>
           <span class="text">只看有内容的评价</span>
          </div>
        </div>
        <div class="ratingall">
            <ul>
              <li v-for="(item,i) in  showRatings" :key="i" class="content1">
                <div class="toux"><img :src="item.avatar" width="30"></div>
                <div class="cmain">
                  <div class="username">{{item.username}}<span>{{times(item.rateTime)}}</span></div>
                  <div class="score" ><span v-html="xin1(item.score)"></span><span>{{item.deliveryTime}}</span></div>
                  <div class="text">{{item.text}}</div>
                  <div class="recommend">
                    <span  v-for="(v,i) in item.recommend" :key="i" >{{v}}</span></div>
                </div>
              </li>
            </ul>
        </div>
     </div>
  </div>
</template>

<script>
export default {
  name: "entry",
  props: ["ratings", "seller"],
  data() {
    return {
      gou:true,
      all:0,
      raclass:"rats allactive",
      manclass:"rats",
      buclass:"rats buman",
      showRatings:[],
      mcount:0,
      ncount:0
    };
  },
  methods: {
    xin(num) {
      var str = "";
      var fnum = Math.floor(num);
      for (var i = 0; i < fnum; i++) {
        str += "<img width='15px'  src='./static/img/xing.png'/>";
      }
      if (num < 5) {
        for (var j = 0; j < 5 - fnum; j++) {
          str += "<img width='15px' src='./static/img/xing1.png'/>";
        }
      }
      return str;
    },
     xin1(num) {
      var str = "";
      var fnum = Math.floor(num);
      for (var i = 0; i < fnum; i++) {
        str += "<img width='12px'  src='./static/img/xing.png'/>";
      }
      if (num < 5) {
        for (var j = 0; j < 5 - fnum; j++) {
          str += "<img width='12px' src='./static/img/xing1.png'/>";
        }
      }
      return str;
    },
    gouc(arr){
      if(this.gou==true){
        this.gou=false;
        //  let arr2=[];
      //   for(let i=0;i<arr.length;i++){
      //   if(arr[i].text!=""){
      //     arr2.push(arr[i]);
      //   }
      // }
      // this.showRatings=arr2;
      }else{
        this.gou=true;
        // this.show(arr)
      }
    },
    change(arr){
      this.raclass="allactive";
      this.manclass="rats";
      this.buclass="rats buman";
      this.show(arr)
    },
    change1(arr){
      this.raclass="rats";
      this.manclass="allactive";
      this.buclass="rats buman";
      let arr2=[];
      for(let i=0;i<arr.length;i++){
        if(arr[i].rateType==0){
          arr2.push(arr[i]);
        }
      }
      this.show(arr2);
    },
     change2(arr){
       this.raclass="rats";
       this.manclass="rats";
       this.buclass="rats bumanactive";
        let arr2=[];
        for(let i=0;i<arr.length;i++){
          if(arr[i].rateType==1){
            arr2.push(arr[i]);
          }
        }
        this.show(arr2);
    },
    show(arr){
      this.showRatings =arr;
    },
    times(str){
      var dat =new Date(str);
				  var datyear =dat.getFullYear();
				  var datmonth =this.addZero(dat.getMonth()+1);
				  var datdate =this.addZero(dat.getDate());
					var dathours =this.addZero(dat.getHours());
					var datminutes =this.addZero(dat.getMinutes());
					var datseconds =this.addZero(dat.getSeconds());
				  var newstr =datyear+"-"+datmonth+"-"+datdate+" "+dathours+":"+datminutes+":"+datseconds ;
				 return newstr;
    },
    addZero(a){
				if(a<10){
					a="0"+a;
				}
				return a
			}
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.ratings{
  overflow-x: hidden;
  margin-top: 175px;
}
.plun {
  display: none;
}
.pfen {
  width: 100%;
  margin-top: 20px;
  display: flex;
}
.pfenleft {
  text-align: center;
  border-right: 1px solid #eee;
  width: 30%;
  padding: 0 15px;
}
.pfen .pfenleft span:first-child {
  display: block;
  height: 20px;
  font-size: 25px;
  color: #ff9d09;
}
.pfen .pfenleft span:last-child {
  font-size: 12px;
  color: #acb1b5;
  display: block;
  margin-top: 15px;
}
.pfen .pfenleft p {
  font-size: 13px;
  height: 5px;
  margin-top: 10px;
}
.pfenright {
  font-size: 12px;
  margin-left: 15px;
}
.pfenright .xing {
  height: 25px;
}
.pfenright .xing div {
  display: inline-block;
}
.pfenright .xing img {
  width: 15px;
  height: 15px;
  margin-left: 3px;
  vertical-align: top;
}
.pfenright .xing span:last-child {
  color: #ff9d09;
}
.pfenright #songd span:last-child {
  color: #c6c6c6;
  margin-left: 5px;
}
.clear {
  width: 100%;
  height: 20px;
  background: #f3f5f7;
  border: 1px solid #c6c6c6;
  margin-top: 20px;
}
.rating-type{
  border-bottom: 1px solid #eee;
  padding: 20px;
}
.switch{
  border-bottom: 1px solid #eee;
  padding: 20px;
  color: #999;
  font-size: 13px;
}
.rats{
  display: inline-block;
  width: 63px;
  height: 32px;
  line-height: 32px;
  background-color: #CCECF8;
  text-align: center;
  color: #666;
  font-size: 13px;
}
.icon{
  display: inline-block;
  width: 20px;
  height: 20px;
  background-image:url("gou.png");
  background-size:20px 20px;
  vertical-align: -5px;  
}
.icon1{
  background-image:url("gou1.png");
}
.buman{
  background-color: #cccccc;
  color: #666;
}
.allactive{
  display: inline-block;
  width: 63px;
  height: 32px;
  line-height: 32px;
  text-align: center;
  font-size: 13px;
  background-color: #00A0DC;
  color: #fff;
}
.bumanactive{
  background-color: #666;
  color: #fff;
}
.content1{
  display: flex;
  padding: 25px 20px; 
  border-bottom: 1px solid #eee;
}
.toux{
  border-radius: 50%;
  width: 30px;
  height: 30px;
  overflow: hidden;
  
}
.cmain{
  flex: 1;
  margin-left: 10px;
}
.username{
  font-size: 13px;
}
.username span{
  font-size: 12px;
  float: right;
  color: #999;
}
.score{
  font-size: 10px;
  color: #999;
  margin: 5px 0px;
}
.score span:last-child{
  margin-left: 10px;
}
.text{
  font-size: 12px;
  height: 20px;
  line-height: 20px;
}
.recommend{
  font-size: 11px;
  margin-top: 20px;
  color: #666;
  display: flex;
  justify-content:flex-start;
  flex-wrap: wrap;
}
.recommend span{
  display: inline-block;
  border: 1px solid #ccc;
  padding: 5px;
  margin-right: 5px;
  margin-top: 5px;
}

</style>
