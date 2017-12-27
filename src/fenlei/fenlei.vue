<template>

	<div id="fenlei">
	  <h1>fenlei</h1>
		<!-- <router-link to="/fenlei/fenleia">多点超市</router-link>
		<router-link to="/fenlei/fenleib">全球精选</router-link>
		<router-view></router-view> -->

    <!-- 左边的列表 -->
    <div class="leftMenu">
      <li :class="{'active':i == index}" v-for="(item,i) in list" @click="dianji(item.siSeq,i)">{{ item.appName }}</li>
    </div>

    <!-- 右边的列表详情 -->
    <div class="rightDetail">
      <div>
        <div v-for="(item,i) in derailList">
          <p class="biaoTi">{{ item.appName }}</p>
          <div class="detailList">
            <li v-for="(item,i) in item.child">
              <img :src="item.icon" alt="">
              <p>{{item.appName}}</p>
            </li>
          </div>
        </div>
      </div>
    </div>
	</div>

</template>

<script>

	export default{
		name:"fenlei",
		data(){
			return{
        index:0,
        list:[],
        derailList:[]
				// aa:[]
				// bb:[],
				// currentIndex:0,
				// currentIndex1:0,
				// currentIndex2:0

			}
		},
		methods:{
			// total(){
			// 		var i = -600;
			// 	var chuxian = setInterval(()=>{

			// 		this.$refs.totalList1.style.bottom= i + 'px';
			// 		i+=10;
			// 		if (i==0){
			// 		clearInterval(chuxian);
			// 		}
			// 		},1);
			// 	this.$refs.zhezhao1.style.display='block';
			// },
			// xiaoshi(){
			// 	var i = 0;
			// 	var chuxian = setInterval(()=>{

			// 		this.$refs.totalList1.style.bottom= i + 'px';
			// 		i-=10;
			// 		if (i==-600){
			// 				clearInterval(chuxian);
			// 		}
			// 	},1);
			// 	this.$refs.zhezhao1.style.display='none';
			// },
			// dianji(i){
			// 	this.aa=this.list[i].childCmCategories;
			// 	this.currentIndex = i;
			// },
      dianji(url,i){
        // 点击的时候调用这个函数，并将参数穿进去
        this.getDataDetail(url)
        this.index = i
      },
      // 这个是拿左边列表的数据
      getData(){
        this.axios({
          url:"https://www.easy-mock.com/mock/59ba12e6e0dc663341a97644/example/firstCategory",
          method:"GET"
        }).then(res=>{
          console.log(res.data.CategoryList)
          this.list =res.data.CategoryList
        })
      },

      // 右边默认显示第一个
      getDataDetailMoRen(){
        this.axios({
          url:"https://www.easy-mock.com/mock/59ba12e6e0dc663341a97644/example/CF100005",
          method:"GET"
        }).then(res=>{
          console.log(res.data.CategoryTree)
          this.derailList = res.data.CategoryTree
        })
      },
      // 这个是拿右边的数据
      getDataDetail(url){
        this.axios({
          url:"https://www.easy-mock.com/mock/59ba12e6e0dc663341a97644/example/"+url,
          method:"GET"
        }).then(res=>{
          console.log(res.data.CategoryTree)
          this.derailList = res.data.CategoryTree
        })
      },
			erDian(item,i){
				this.bb = item.childCmCategories;
				this.currentIndex1 = i;
				},
			sandian(i){
				this.currentIndex2 = i;
			}
		},

		// },
		created(){
      this.getData()
      // 拿默认数据
      this.getDataDetailMoRen()
		}

	}

</script>

<style>
/* 从这里 */
  .leftMenu{
    width: 100px;
    height: 500px;
    background: #fff;
    float: left;
  }
  .leftMenu li{
    height: 30px;
    text-align: center;
    line-height: 30px;
    list-style: none;
    border-bottom: 1px solid #aaa;
  }
  .rightDetail{
    width: 250px;
    height: 500px;
    float: left;
    background: #fff;
    margin-left: 20px;
    overflow: scroll;
  }
  .rightDetail li{
    list-style: none;
  }
  .biaoTi{
    height: 40px;
    width: 100%;
    line-height: 40px;
    margin-left: 20px;
  }
  .detailList{
    display: flex;
    flex-wrap: wrap;
    font-size: 12px;
    color: #aaa;
  }
  .detailList li{
    width: 30%;
    text-align: center;
  }
  .detailList li img{
    width: 50px;
    height: 50px;
  }
/* 到这里 */




	#fenlei .header {
		width: 100%;
		height: 5rem;
	}
	#fenlei .header p{
		width: 100%;
		height: 5rem;
		background:url(../assets/vipimg/1.png) no-repeat left center;
		background-size: 100% auto;
	}
	#fenlei .tiao{
		width: 100%;
		height: 0.5rem;
		background:#fef2de;
		font-size: 0.3rem;
	}
	#fenlei .tiao p{
		padding: 0.05rem 0 0 0.25rem;
	}
	#fenlei .totalList{
		width: 100%;
		height:15rem;
		background: white;
		position: fixed;
		bottom: -15rem;
		z-index: 3;

	}
	#fenlei .zhezhao{
		height: 100%;
		width: 100%;
		background: rgba(0,0,0,.5);
		position: fixed;
		top: 0;
		left: 0;
		z-index: 2;
		display: none;
	}
	#fenlei .tou{
		display: flex;
		height: 1.1rem;
		line-height: 1.1rem;
		justify-content: space-between;
		border-bottom: 1px solid #f3f3f3;
	}
	#fenlei .tou span:nth-child(2){
		color: #f4f4f4;
	}
	#fenlei .xiabian{
		display: flex;

	}
	#fenlei .totalList .left{
		width: 33.33%;
		height: 14.9rem;
	}
	#fenlei .totalList .middle{
		width: 33.33%;
		height: 14.9rem;
		background: #f6f6f6;
	}
	#fenlei .totalList .right{
		width: 33.33%;
		height: 14.9rem;
		background: #f0f0f0;
	}
	#fenlei .totalList .left li{
		width: 3.125rem;
		height: 1.1rem;
		text-align: center;
		line-height: 1.1rem;
	}
	#fenlei .middle li{
		width: 3.125rem;
		height: 1.1rem;
		line-height: 1.1rem;
		text-align: center;
	}
	#fenlei .right li{
		width: 3.125rem;
		height: 1.1rem;
		line-height: 1.1rem;
		text-align: center;
	}
	#fenlei .active{
		border-left: 2px solid #ff712b;
		color: #ff712b;
		background: #f6f6f6;
	}
	#fenlei .active1{
		background: #f0f0f0;
		color: #ff712b;
	}
	#fenlei .active2{
		background: #ebebeb;
		color: #ff712b;
	}
</style>
