<template >
    <div>
        <!-- 轮播图 start-->
        <lbt-box :Lunbotulist="Lunbotulist" :isfull="true"></lbt-box>
        <!-- <mt-swipe :auto="4000"> -->
            <!-- 该item里面不含有id属性，故用key绑定url，要绑定的是该item中的值 -->
            <!-- <mt-swipe-item v-for="item in LunbotuList" :key="item.url"-->
                <!-- <img :src="item.img"-->
            <!-- </mt-swipe-item>     -->
        <!-- </mt-swipe>   -->
        <!-- 轮播图结束 -->
        <!-- 九宫格改造为6宫格开始 -->
        
		    <ul class="mui-table-view mui-grid-view mui-grid-9">
		        <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link to="/home/newslist">
		                <img src="../images/menu1.png" alt="">
		                <div class="mui-media-body">新闻资讯</div></router-link></li>
		        <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link to="/home/photolist">
		                <img src="../images/menu2.png" alt="">
		                <div class="mui-media-body">图片分享</div></router-link></li>
		        <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link  to="/home/goodslist">
		                <img src="../images/menu3.png" alt="">
		                <div class="mui-media-body">商品购买</div></router-link ></li>
		        <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link  to="/home/">
		                <img src="../images/menu4.png" alt="">
		                <div class="mui-media-body">留言反馈</div></router-link ></li>
		        <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link  to="/home/">
		                <img src="../images/menu5.png" alt="">
		                <div class="mui-media-body">视觉专区</div></router-link ></li>
		        <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link  to="/home/">
		                <img src="../images/menu6.png" alt="">
		                <div class="mui-media-body">联系我们</div></router-link ></li>

		    </ul> 
		
        <!-- 6宫格结束 -->

    </div>
</template>
<script>

import Lunbotu from './subcomponent/Lunbotu.vue'

export default {
    data(){
        return{
            LunbotuList:[],

        }
    },
    methods:{
        getLunbotu(){
            // 获取轮播图数据的方法
            this.$http.get('api/getlunbo').then(response => {console.log(response.body)})
            // 回传的数据response其中的body中有个状态status及message数组，其中包含着一些对象，每个对象包含该图片地址及点击该图片要跳转到的地址
            if(response.body.status === 0){
                this.LunbotuList= response.body.message;
            }else{
                Toast("加载轮播图失败")

            }
        }

    },
    created(){
        this.getLunbotu();
    },components:{
        'lbt-box':Lunbotu,
    }
    
}
</script>
<style lang="scss" scoped>


.mui-grid-view .mui-grid-9{
    background-color: #fff;
    border:none;
    img{
        width:60px;
        height: 60px;
    }
    .mui-media-body{
        font-size: 13px;
    }
}
.mui-grid-view .mui-grid-9 .mui-table-view-cell{
    background-color: #fff;
    border: none;

}
</style>


