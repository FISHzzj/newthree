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
            <div class="item flex ali_center">
                <div class="content">
                    <p>【精彩实录】FIce官方哈色第六届had盛放假熬枯受淡</p>
                    <p>2020-10-10 22:24:20</p>
                </div>
                <div class="img"><img src="http://193.112.106.104:902/attachment/images/1/2021/04/eXlLwZf2X2R2MMdf2HnzMNDqY5gYFd.png" alt=""></div>
            </div>
            <div class="item flex ali_center">
                <div class="content">
                    <p>【精彩实录】FIce官方哈色第六届had盛放假熬枯受淡</p>
                    <p>2020-10-10 22:24:20</p>
                </div>
                <div class="img"><img src="http://193.112.106.104:902/attachment/images/1/2021/04/eXlLwZf2X2R2MMdf2HnzMNDqY5gYFd.png" alt=""></div>
            </div>
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
        }
    },
    mounted() {
        this.getlist()
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
    }
}
</script>
<style lang="less" scoped>
.informa{
    background-color: #F4F4F4!important;
    .mySwiper {
        .swiper-container {
            background: #ccc;
        }
        .pagination-bullet-active {
            color: #000000!important;
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
                background: #000;
            }
            p {
                font-size: 4.2vw;
                font-weight: 600;
            }
        }
        .item{
            background: #FEFEFE;
            border-bottom: 1px solid #eee;
            margin-bottom: 10px;
            .content{
                margin-right: 10px;
                padding: 0 5px;
                p:nth-child(1){
                    font-weight: 500;
                    font-size: 14px;
                    color: #000;
                    margin-bottom: 10px;
                }
                p:nth-child(2){
                    color: #ccc;
                    font-size: 12px;
                }
            }
            .img{
                img{
                    height: 120px;
                    width: 170px;
                }
            }
        }
    }
}

</style>


