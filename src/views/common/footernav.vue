<template>
    <div class="footer">
        <div style="height:12vw;"></div>
        <div class="nav_1 flex ali_center">
            <div @click="goitem(item)" class="item flex ali_center" v-for="(item, index) in list" :key="index">
                <img :src="$route.path == item.url ? item.img_sel : item.img" alt="">
                <p :class="{on: $route.path == item.url}">{{item.name}}</p>
            </div>
        </div>
        <service
            :showService="showService"
            @close="closeservice"
        ></service>
    </div>
    
</template>
<script>
import service from "../common/service";
export default {
    name: "footernav",
    components:{
        service
    },
    data() {
        return {
            showService: false,
            list: [
                {
                    name: "首页",
                    img:  require('@/assets/images/home/home.png'),
                    img_sel:  require('@/assets/images/home/home_sel.png'),
                    url: "/index"
                },
                {
                    name: "资讯",
                    img:  require('@/assets/images/home/informa.png'),
                    img_sel:  require('@/assets/images/home/informa_sel.png'),
                    url: "/informa"
                },
                {
                    name: "客服",
                    img:  require('@/assets/images/home/server.png'),
                    img_sel:  require('@/assets/images/home/server_sel.png'),
                    url: "/server"
                },
                {
                    name: "我的",
                    img:  require('@/assets/images/home/user.png'),
                    img_sel:  require('@/assets/images/home/user_sel.png'),
                    url: "/user"
                }
            ]
        };
    },
    mounted() {
        console.log(this.$route.path);
    },
    methods: {
        closeservice(e) {
            this.showService = false;
        },
        goitem(e) {
            if(e.url == '/server') {
                this.showService = true;
            }else{
                this.$router.push({
                    path: e.url
                });
            }
            
        }
    }
}
</script>
<style lang="less" scoped>
.footer {
    .nav_1 {
        position: fixed;
        background: #fff;
        bottom: 0;
        left: 0;
        width: 100%;
        height: 12vw;
        z-index: 10000;
        flex-wrap: nowrap;
        .item {
            width: 33vw;
            flex-direction: column;
            justify-content: center;
            img {
                width: 5.33vw;
                height: 5.33vw;
            }
            p {
                font-size: 3.2vw;
                color: #999;
                &.on {
                    color: #333;
                }
            }
        }
    }
}
</style>