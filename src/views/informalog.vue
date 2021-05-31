<template>
    <div class="informalog">
        <div class="header">
            <van-icon @click="$router.go(-1)" name="arrow-left" size="20" />
            <p>新闻内容</p>
        </div>
        <div><img :src="thumb" alt=""></div>
        <div v-html="detail">

        </div>
        
    </div>
</template>
<script>
export default {
    name: "informalog",
    data() {
        return {
            id: 0,
            custMobile: "",
            wechat_name: "",
            content: "",
            wechat_img: "",
            title: "",
            thumb: "",
            detail: "",
            createtime: "",
        };
    },
    mounted() {
        this.id = this.$route.query.id;
        console.log(this.id);
        this.getlist(this.id)
    },
    methods:{
         async getlist(id){
            let res = await $ajax('kuangfooterlog', {id: id})
            if (!res) return false
            this.title = res.title
            this.thumb = res.thumb
            this.detail = res.detail
            this.createtime = res.createtime
            // this.custMobile = res.custMobile
            // this.wechat_name = res.wechat_name
            // this.content = res.content
            // this.wechat_img = res.wechat_img
            
        },
    }
};
</script>
<style lang="less" scoped>
.informalog {
    .header {
        width: 100%;
        height: 12vw;
        position: relative;
        .van-icon {
            position: absolute;
            top: 0;
            left: 3vw;
            bottom: 0;
            height: 4vw;
            margin: auto 0;
        }
        p {
            width: 100%;
            line-height: 12vw;
            font-size: 4vw;
            text-align: center;
        }
    }
}
</style>