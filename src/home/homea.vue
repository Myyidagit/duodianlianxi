<template>

	<div id="homea">

		<!-- <router-link to="/home_xian">home_xian</router-link>
		<router-view></router-view> -->
		<!-- <h1>好么</h1> -->
		<!-- ~~~~~~~~~~~~~~~~~~~~~轮播图~~~~~~~~~~~~~~~~~~~~~ -->
		<div class="homeaLunbo">
			<swiper :options="swiperOption" >
				<!-- 遍历轮播图片 -->
			    <swiper-slide v-for="item in data">
			        <img v-lazy="item.imageUrl">
			    </swiper-slide>
			    <!-- 分页器 -->
			    <div class="swiper-pagination" slot="pagination"></div>
			</swiper>
		</div>
		<!-- ~~~~~~~~~~~~~~~~~~~~~好货提前抢~~~~~~~~~~~~~~~~~~~~~ -->
		<!-- <ul class="homeaBlock">
			<li v-for="item in aa " class="homeaBlockLi">
				<router-link to="/good">
					<img v-bindv-lazy="item.imageUrl" alt="" class="homeaBlockLiImg">
					<p>{{item.data.title}}</p>
				</router-link>
				<router-view></router-view>
			</li>
		</ul> -->
		<hao :list="datah"></hao>
		<!-- ~~~~~~~~~~~~~~~~~~~~精选推荐~~~~~~~~~~~~~~~~~~~~ -->
		<div v-for="p in dataj" class="jingxuan">
			<img v-lazy="p.imageUrl" alt="" class="jingImg">
		</div>
		<!-- ~~~~~~~~~~~~~~~~~~~生鲜集结号~~~~~~~~~~~~~~~~~~~~~~·~~~ -->
		<div v-for="p, i in datas" :class="{'first': i == 0}" class="shengxian">
			<router-link to="/home_xian">
				<img v-lazy="p.imageUrl">
			</router-link>
			<router-view></router-view>
		</div>
		<!-- ~~~~~~~~~~~~~~~~~~~~~~~~~超市优选~~~~~~~~~~~~~~~~~~~~ -->
		<div v-for="p in datai" class="chaoshi">
			<img v-lazy="p.imageUrl" alt="">
		</div>
		<!-- ~~~~~~~~~~~~~~~~~~~~~~~~~鲜菜~~~~~~~~~~~~~~~~~~~~ -->
		<div class="xiancai clear">
			<div v-for="p in datax" >
				<img v-lazy="p.imageUrl" alt="">
			</div>
			<div v-for="p in datal" >
				<img v-lazy="p.imageUrl" alt="">
			</div>
		</div>
		<!-- ~~~~~~~~~~~~~~~~~~~~~~~~健康蔬菜~~~~~~~~~~~~~~~~~~~~~~ -->
		<div v-for="p in datajk" class="shucai">
			<img v-lazy="p.imageUrl" alt="">
		</div>
		<!-- ~~~~~~~~~~~~~~~~~~~~~~~~健康蔬菜下的瓜果~~~~~~~~~~~~~~~~~~ -->
		<div class="jiankang">
			<ul class="jiankangUl">
				<li v-for="p in dataguan" class="jiankangli">
					<img v-bind:src="p.imageUrl" alt="" @click='store(p)'>
					<p class="jiankangInfo">{{ p.data.name}}</p>
					<del class="jiankangDel">{{ p.data.price}}</del>
					<p class="jiankangNew">{{ p.data.promotionPrice}}</p>
					<p class="jia" @click='addGoods(p)'>+</p>
				</li>
			</ul>
		</div>
		<div class="kong"></div>
	</div>

</template>

<script>
	// 引入轮播图组件
	import Hao from './hao.vue'
	export default{
		name:"homea",
		props:["items"],
		// 注册轮播图组件
		components:{ Hao },
		data(){
			return{
        data:[],
				datah:[],   //好货提前抢的数据
				dataj:[],   //精选
				datas:[],   //生鲜
				datai:[],   //超市优选
				datax:[],   //鲜菜鲜果
				datal:[],   //粮油副食
				datajk:[],  //健康蔬菜
				dataguan:[], //瓜果

				swiperOption: {
		            autoplay: 1000,  //1秒
		            direction : 'horizontal', //横向
		            pagination : '.swiper-pagination',
		        }
			}
		},
		methods:{
			store(item){
				//将对象添加到详情
				this.$store.commit('ADD_MONEY',item);


				this.$router.push({
					//路由的名字
					name:'goodDetil',
					path:{

					}
				})
			},
			addGoods(item){
				//将商品添加到购物车
				this.$store.commit('ADD_GOODS',item);
				//点击添加商品的同时将价格加在money上
				this.$store.commit('ADD_PRICE',item);
			}
		},
		created(){  //组件创建完成即可发起网络请求
			this.axios.get("../../static/duoDian.json").then(res => {
				// console.log(res.data.data.pageModules[0].dataList)
				// console.log(res.data.data.pageModules[2].dataList)
				// console.log(res.data.data.pageModules[9].dataList)
				this.data = res.data.data.pageModules[0].dataList
				this.datah = res.data.data.pageModules[2].dataList
				console.log(this.datah)
				this.dataj = res.data.data.pageModules[3].dataList
				this.datas = res.data.data.pageModules[4].dataList
				this.datai = res.data.data.pageModules[5].dataList
				this.datax = res.data.data.pageModules[6].dataList
				this.datal = res.data.data.pageModules[7].dataList
				this.datajk = res.data.data.pageModules[8].dataList
				this.dataguan = res.data.data.pageModules[9].dataList

			})


		},
		computed: {
			// aa() {  //添加方法
			// 	this.datah.splice(5, 1);
			// 	return this.datah;
			// }
			// return aa.filters(function(item){
			// 	return item.age >= 18;
			// })

		},
		// filters:{  //过滤器
		// 	aa( datah, b ){
		// 		const arr = [];
		// 		datah.splice(b, 1);
		// 		datah.map(item => {
		// 			arr.push(item);

		// 		});
		// 		return arr;
		// 	}
		// }

	}

</script>

<style scoped>
	#homea{
		background: #F6F6F6;

	}
	#homea h1{
		color:blue;
	}
	.homeaLunbo{
		width: 100%;
		height: 3.75rem;
		/*background: yellow;*/
	}
	.homeaLunbo img{
		width: 100%;
		height: 3.75rem;
	}

	/*---------------好货提前抢-------------*/

	/*-------------------精选推荐--------------*/
	.jingxuan{
		width: 100%;
		height: 2.2125rem;

	}
	.jingImg{
		width: 100%;
		height: 2.2125rem;
	}
	/*------------------生鲜集结号---------------*/
	.shengxian img {
		width: 4.675rem;
		height: 2.75rem;
		float:left;
	}
	.first img {
		width: 4.675rem;
		height: 5.5rem;
	}

	/*------------------超市优选-------------------*/
	.chaoshi img{
		width: 100%;
		height: 1.5rem;
	}

	/*-------------------鲜菜------------------*/
	.xiancai{
		width: 100%;

	}
	.xiancai img{
		width: 3.125rem;
		height: 3.75rem;
		float: left;
	}
	/*----------------------健康蔬菜--------------*/
	.shucai img{
		margin-top: 10px;
		width: 100%;
		height:2.875rem;
	}
	/*----------------健康蔬菜下的瓜果-------------*/
	.jiankangUl{
		width: 100%;
		display: flex;
		justify-content:space-around;
		align-items:center;
		flex-wrap:wrap;

	}
	.jiankangUl>li{
		/*float: left;*/
	}
	.jiankangli{
		width: 3.125rem;
		height:5.825rem;
		background-color: #fff;
		padding:0.25rem 0.15rem;
		position: relative;
	}
	.jiankangli p{
		color:#888;
		padding-left:0.25rem;
	}
	.jiankangli p:nth-of-type(2){
		color:#FF712B;
	}
	.jiankangli>img{
		width: 2.875rem;
		height:2.875rem;
	}
	.jiankangInfo{
		width:2.625rem;
		height: 0.9rem;
	}
	.jiankangDel{
		color: #888;
		padding-left:0.25rem;
	}
	.jiankangli p:nth-of-type(3){
		width: 0.75rem;
		height: 0.5rem;
		line-height: 0.5rem;
		/*text-align: center;*/
		color:#FF712B;
		border:1px solid #FF712B;
		position: absolute;
		bottom:0.825rem;
		right: 0.5rem;
	}

	.kong{
		width: 100%;
		height: 1.25rem;
	}

</style>
