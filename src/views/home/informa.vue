<template>
    <div class="informa">
        <!-- 资讯轮播 -->
        <swiper ref="mySwiper" class="mySwiper" :options="swiperOptions">
            <swiper-slide v-for="(item, index) in banner" :key="index">
                <a :href="item.url">
                    <img :src="item.img" alt="">
                </a>
            </swiper-slide>
            <div class="swiper-pagination" slot="pagination"></div>
        </swiper>
        <!-- 数据 -->
        <section class="wrapper">
            <div class="title flex ali_center">
                <!-- <img src="@/assets/images/home/laba2.jpg" alt=""> -->
                <p>最新资讯</p>
            </div>
            <div class="item flex ali_center" v-for="(item, index) in foooter" :key="index" @click="gonext(item.id)" >
                <div class="content">
                    <p>{{item.title}}</p>
                    <p>{{item.createtime}}</p>
                </div>
                <div class="img"><img :src="item.thumb" alt=""></div>
            </div>
            <!-- <div class="item flex ali_center">
                <div class="content">
                    <p>【精彩实录】FIce官方哈色第六届had盛放假熬枯受淡</p>
                    <p>2020-10-10 22:24:20</p>
                </div>
                <div class="img"><img src="http://193.112.106.104:902/attachment/images/1/2021/04/eXlLwZf2X2R2MMdf2HnzMNDqY5gYFd.png" alt=""></div>
            </div> -->
        </section>
        <bottom-nav></bottom-nav>
    </div>
</template>
<script>
import bottomNav from "../common/footernav";
import { swiper, swiperSlide } from "vue-awesome-swiper";
import "swiper/swiper-bundle.css";
export default {
    name: "informa",
    components: {
        bottomNav,
        swiper,
        swiperSlide,
    },
    data() {
        return {
            banner:[],
            swiperOptions: {
                loop: true,
                speed: 2000,
                autoplay: {
                    delay: 3000,
                    stopOnLastSlide: false,
                    disableOnInteraction: false,
                },
                // 显示分页
                pagination: {
                    el: ".swiper-pagination",
                    clickable: true, //允许分页点击跳转
                },
            },
            foooter:[]
        }
    },
    mounted() {
        this.getlist()
        this.getfooter()
    },
    methods:{
        async getlist(){
            let res = await $ajax('kuang', {})
            if (!res) return false
            this.banner = res.banner
            // this.bannerTxt = res.bannerTxt
            // this.btc = res.btc
            // this.eth = res.eth
            // this.fil = res.fil
            // this.xch = res.xch
            // this.footer = res.footer
            // this.btc_url = res.btc_url
            // this.eth_url = res.eth_url
            // this.fil_url = res.fil_url
            // this.xch_url = res.xch_url
            
        },
        async getfooter(data){
            let res = await $ajax('kuangfooter', {})
            if (!res) return false
            this.foooter = res.foooter
        },
        gonext(id){
            console.log(id)
            this.$router.push({
                name: 'informalog',
                query:{
                    id
                }
            })
        }
    }
}
</script>
<style lang="less" scoped>
.informa{
    background-color: #f7f7f7!important;
    .mySwiper {
        .swiper-container {
            background: #ccc;
        }
        .pagination-bullet-active {
            color: #f7f7f7!important;
        }
        .swiper-slide {
            height: 50vw;
            img {
                width:100vw;
                height: 50vw;
            }
        }
    }
    .wrapper {
        padding: 0 4vw;
        .title {
            height: 12vw;
            img {
                width: 5.33vw;
                height: 5.33vw;
                margin-right: 2.4vw;
                background: #f7f7f7;
            }
            p {
                font-size: 4.2vw;
                font-weight: 600;
            }
        }
        .item{
             box-shadow: 2px 2px 2px 1px #e4e0e0;
            background: #eee;
            border-bottom: 1px solid #eee;
            margin-bottom: 10px;
            border-radius: 10px;
            .content{
                margin-right: 10px;
                padding: 0 5px;
                width: 155px;
                p:nth-child(1){
                    font-weight: 500;
                    font-size: 14px;
                    color: #000;
                    margin-bottom: 10px;
                }
                p:nth-child(2){
                    color: #333;
                    font-size: 12px;
                }
            }
            .img{
                img{
                    height: 120px;
                    width: 170px;
                    border-radius: 10px;
                }
            }
        }
    }
}

</style>


