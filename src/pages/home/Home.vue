<template>
    <div>
        <home-header></home-header>
        <home-swiper :list="swiperList"></home-swiper>
        <home-icons :iconList="iconList"></home-icons>
        <home-recommend :recommendList="recommendList"></home-recommend>
        <home-weekend :weekendList="weekendList"></home-weekend>
    </div>
</template>


<script>
import HomeHeader from './components/Header'
import HomeSwiper from './components/Swiper'
import HomeIcons from './components/Icons'
import HomeRecommend from './components/Recommend'
import HomeWeekend from './components/Weekend'
import axios from 'axios'
export default {
    name:'Home',
    data(){
        return{
            swiperList:[],
            iconList:[],
            recommendList:[],
            weekendList:[]
        }
    },
    components:{
        HomeHeader,
        HomeSwiper,
        HomeIcons,
        HomeRecommend,
        HomeWeekend
    },
    methods:{
        getHomeInfo(){
            axios.get('/api/index.json')
                .then(this.getHomeInfoSucc) //接收一个promiss对象
        },
        getHomeInfoSucc(res){
           res = res.data
           if(res.ret && res.data){
               this.swiperList = res.data.swiperList
               this.iconList = res.data.iconList
               this.recommendList = res.data.recommendList
               this.weekendList = res.data.weekendList
           }
        }
    },
    mounted () {
        this.getHomeInfo()
    }
    
}
</script>

<style scoped>

</style>


