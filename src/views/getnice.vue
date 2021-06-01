<template>
    <div class="getnice">
        <div class="header">
            <van-icon @click="$router.go(-1)" name="arrow-left" size="20" />
            <p>收益记录</p>
        </div>
        <div class="nav flex ali_center">
            <div class="item" @click="changenav(index)" :class="{on:index == status}" v-for="(item, index) in navlist" :key="index">
                {{item}}
            </div>
        </div>
        <div class="teaminfo">
            <div class="nav flex ali_center">
                <div class="item">
                    <div class="type">{{nameunit0}}</div>
                    <div class="num">{{countMoney}}</div>
                </div>
                <div class="item">
                    <div class="type">{{nameunit}}</div>
                    <div class="num">{{noDayMoney}}</div>
                </div>
            </div>
        </div>
        <div class="list" >
            <van-list
                v-model="loading"
                :finished="finished"
                :finished-text="'我是有底线的'"
                @load="logs"
                >
                <div
                class="item flex ali_center flex_between" 
               
                v-for="(item,index) in list" :key="index">
                    
                    <div class="left">
                        <div class="type">{{item.rechargeType}}</div>
                        <div class="time">{{item.createtime}}</div>
                    </div>
                    <div class="right">{{item.money}}</div>
                </div >
              
            </van-list>
           
        </div>
    </div>
</template>
<script>
export default {
    name: "getnice",
    data() {
        return {
            title: '',
            status: 0,
            navlist: ['推荐奖励', '挖矿奖励'],
            typenum: 1,
            list: [],
            page: 1,
            limit: 10,
            finished: false,
            loading: false,
            levelType: 1,
            countMoney: "",
            noDayMoney: "",
            nameunit0:"累积奖励（XCH）",
            nameunit:"累积奖励（USDT）",

        };
    },
    mounted() {
        // this.type = this.$route.params.type;
        // if (this.type =='recharge') {
        //     this.title = "充值记录"
        //     this.typenum = 1
        //     // this.logs()
        // } else if (this.type == "cash") {
        //     this.title = "提现记录"
        //     this.typenum = 2
        // }else if (this.type == "duihuan"){
        //     this.typenum = 3
        // }
    },
    methods: {
        changenav(index) {
            this.status = index;
            if(index == 0 ){ //推荐奖励
                this.status = ""
                this.page = 1
                this.list = []
                this.levelType = 'push'
                this.logs()
                // this.unit0 = ''
                // this.unit = ''
                this.nameunit0 = '累积奖励(XCH)'
                this.nameunit = '累积奖励(USDT)'
            }else if(index == 1) { //挖矿奖励
                this.status == index
                this.page = 1
                this.list = []
                this.levelType = 'rate'
                this.logs()
                // this.unit0 = 'XCH'
                // this.unit = 'XCH'
                this.nameunit0 = '累积产币(XCH)'
                this.nameunit = '昨日产币(XCH)'
            }
        },
        async logs() {
   
            let res = await $ajax('userlog', {rechargetype : this.levelType})  //充值
            if(!res) return false
            console.log(res)
            // this.money = res.money
           this.countMoney = res.countMoney
           this.noDayMoney = res.noDayMoney
            this.page++
            console.log(res.list)
            this.list.push(...res.list)
            // // 加载状态结束
            this.loading = false
            if (res.list.length === 0) {
                this.finished = true //加载完成
            } 
        },
        gonext(id, text){
            //  :to="{name:'recordDetail', query: {id: item.id}}"
            if(text == '待充值'){
                this.$router.push({
                    name: 'huiMoney',
                    query: {id: id}
                })
            }else{
                 this.$router.push({
                    name: 'recordDetail',
                    query: {id: id}
                })
            }
        }
    }
};
</script>
<style lang="less" scoped>
* {
    box-sizing: border-box;
}
.getnice {
    background: #f7f7f7 !important;
    .header {
        width: 100%;
        height: 12vw;
        background: #fff;
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
    .nav {
        flex-wrap: nowrap;
        height: 12vw;
        background: #fff;
        .item {
            width: 50%;
            text-align: center;
            color: #666;
            font-size: 4vw;
            &.on {
                position: relative;
                color: #000;
                font-size: 4.2vw;
                &::after {
                    position: absolute;
                    content: "";
                    left: 0;
                    right: 0;
                    bottom: -2vw;
                    margin: 0 auto;
                    width: 8vw;
                    height: 0.75vw;
                    background: #6200A5;
                }
            }
        }
    }
    .teaminfo {
        width: 92vw;
        margin: 4vw 4vw 4vw;
        background: #fff;
        border-radius: 2vw;
        text-align: center;
        height:30vw;
        .infos {
            .title {
                line-height: 12vw;
                color: #777;
                font-size: 3.73vw;
            }
            .num {
                color: #999;
                font-size: 3.2vw;
                span {
                    color: #333;
                    font-size: 6vw;
                    font-weight: 600;
                }
            }
        }
        .nav {
            padding: 0 4vw 6vw;
            flex-direction: column;
            .item {
                width: 100%;
                text-align: center;
                color: #666;
                font-size: 4vw;
                margin-top: 2vw;
                .type{
                    font-size: 4vw;
                }
                .num{
                    font-size: 6vw;
                }
                // &.on {
                //     position: relative;
                //     color: #000;
                //     font-size: 4.2vw;
                //     &::after {
                //         position: absolute;
                //         content: "";
                //         left: 0;
                //         right: 0;
                //         bottom: -2vw;
                //         margin: 0 auto;
                //         width: 8vw;
                //         height: 0.75vw;
                //         background: #6200A5;
                //     }
                // }
            }
        }
    }
    .list {
        padding: 4vw;
        .item {
            background: #fff;
            border-radius: 2vw;
            padding: 2vw 2vw;
            margin-bottom: 2.4vw;
           .left {
                .type {
                    font-size: 3.73vw;
                    color: #333;
                }
                .time {
                    margin-top: 1.5vw;
                    color: #999;
                    font-size: 3.2vw;
                }
            }
            .right {
                color: #999;
            }
          
        }
    }
}
</style>