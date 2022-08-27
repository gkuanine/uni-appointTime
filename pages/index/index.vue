<template>
    <view style="display:flex;flex-direction:column;">
        <view style="display:flex;flex-direction:row;justify-content:center; height:45px;text-align:center;line-height:45px;"
              @click="openChooseTime">{{datetime==''?"选择时间":dateStr}}
        </view>
        <appointTime v-on:closeChooseTime="closeChooseTime" v-on:chooseTimeResult="chooseTimeResult"
                     v-show="showChooseTime" style="height:100%; position:fixed;bottom:0px;left:0px;" ref="appointTime"
                     :timeList="simpleCart.dateWeekDeliveryTimeList" :datetime="datetime"></appointTime>
    </view>
</template>

<script>
    import appointTime from '../../components/appointTime.vue'

    var that;
    export default {
        components: {
            appointTime
        },
        data() {
            return {
                title: 'Hello',
                datetime: "",
                dateStr: "",
                showChooseTime: false,
                //购物车数据
                simpleCart: {
                    allCart: [],
                    cartTotal: {
                        checked: 0,
                        checkedProductAmount: 0,
                        checkedProductCount: 0,
                        productAmount: "0.00",
                        productCount: 0
                    },
                    timeList: {},
                    dateWeekDeliveryTimeList: []
                },
            }
        },
        onLoad() {
            var s = `{
    "dateWeekDeliveryTimeList": [
        {
            "cnDateWeekDay": "今天(08-27 周六)",
            "datetime": "2022-08-27 16:35",
            "cnDate": "今天",
            "ymd": "2022-08-27",
            "list": [
                {
                    "cnDay": "周六",
                    "cnDate": "今天",
                    "cnDateWeekDay": "今天(08-27 周六)",
                    "ymd": "2022-08-27",
                    "time": "立即送出",
                    "timeStr": "立即送出",
                    "datetime": "2022-08-27 16:35",
                    "date": 1661589352093
                },
                {
                    "cnDay": "周六",
                    "cnDate": "今天",
                    "cnDateWeekDay": "今天(08-27 周六)",
                    "ymd": "2022-08-27",
                    "time": "17:00",
                    "timeStr": "17:00-17:30",
                    "datetime": "2022-08-27 17:00",
                    "date": 1661590852000
                },
                {
                    "cnDay": "周六",
                    "cnDate": "今天",
                    "cnDateWeekDay": "今天(08-27 周六)",
                    "ymd": "2022-08-27",
                    "time": "17:30",
                    "timeStr": "17:30-18:00",
                    "datetime": "2022-08-27 17:30",
                    "date": 1661592652000
                },
                {
                    "cnDay": "周六",
                    "cnDate": "今天",
                    "cnDateWeekDay": "今天(08-27 周六)",
                    "ymd": "2022-08-27",
                    "time": "18:30",
                    "timeStr": "18:30-19:00",
                    "datetime": "2022-08-27 18:30",
                    "date": 1661596252000
                },
                {
                    "cnDay": "周六",
                    "cnDate": "今天",
                    "cnDateWeekDay": "今天(08-27 周六)",
                    "ymd": "2022-08-27",
                    "time": "19:30",
                    "timeStr": "19:30-20:00",
                    "datetime": "2022-08-27 19:30",
                    "date": 1661599852000
                },
                {
                    "cnDay": "周六",
                    "cnDate": "今天",
                    "cnDateWeekDay": "今天(08-27 周六)",
                    "ymd": "2022-08-27",
                    "time": "20:30",
                    "timeStr": "20:30-21:00",
                    "datetime": "2022-08-27 20:30",
                    "date": 1661603452000
                },
                {
                    "cnDay": "周六",
                    "cnDate": "今天",
                    "cnDateWeekDay": "今天(08-27 周六)",
                    "ymd": "2022-08-27",
                    "time": "21:30",
                    "timeStr": "21:30-22:00",
                    "datetime": "2022-08-27 21:30",
                    "date": 1661607052000
                },
                {
                    "cnDay": "周六",
                    "cnDate": "今天",
                    "cnDateWeekDay": "今天(08-27 周六)",
                    "ymd": "2022-08-27",
                    "time": "22:30",
                    "timeStr": "22:30-23:00",
                    "datetime": "2022-08-27 22:30",
                    "date": 1661610652000
                }
            ]
        },
        {
            "cnDateWeekDay": "明天(08-28 周日)",
            "datetime": "2022-08-28 07:30",
            "cnDate": "明天",
            "ymd": "2022-08-28",
            "list": [
                {
                    "cnDay": "周日",
                    "cnDate": "明天",
                    "cnDateWeekDay": "明天(08-28 周日)",
                    "ymd": "2022-08-28",
                    "time": "07:30",
                    "timeStr": "07:30-08:00",
                    "datetime": "2022-08-28 07:30",
                    "date": 1661643052000
                },
                {
                    "cnDay": "周日",
                    "cnDate": "明天",
                    "cnDateWeekDay": "明天(08-28 周日)",
                    "ymd": "2022-08-28",
                    "time": "08:30",
                    "timeStr": "08:30-09:00",
                    "datetime": "2022-08-28 08:30",
                    "date": 1661646652000
                },
                {
                    "cnDay": "周日",
                    "cnDate": "明天",
                    "cnDateWeekDay": "明天(08-28 周日)",
                    "ymd": "2022-08-28",
                    "time": "09:30",
                    "timeStr": "09:30-10:00",
                    "datetime": "2022-08-28 09:30",
                    "date": 1661650252000
                },
                {
                    "cnDay": "周日",
                    "cnDate": "明天",
                    "cnDateWeekDay": "明天(08-28 周日)",
                    "ymd": "2022-08-28",
                    "time": "10:30",
                    "timeStr": "10:30-11:00",
                    "datetime": "2022-08-28 10:30",
                    "date": 1661653852000
                },
                {
                    "cnDay": "周日",
                    "cnDate": "明天",
                    "cnDateWeekDay": "明天(08-28 周日)",
                    "ymd": "2022-08-28",
                    "time": "11:30",
                    "timeStr": "11:30-12:00",
                    "datetime": "2022-08-28 11:30",
                    "date": 1661657452000
                },
                {
                    "cnDay": "周日",
                    "cnDate": "明天",
                    "cnDateWeekDay": "明天(08-28 周日)",
                    "ymd": "2022-08-28",
                    "time": "12:30",
                    "timeStr": "12:30-13:00",
                    "datetime": "2022-08-28 12:30",
                    "date": 1661661052000
                },
                {
                    "cnDay": "周日",
                    "cnDate": "明天",
                    "cnDateWeekDay": "明天(08-28 周日)",
                    "ymd": "2022-08-28",
                    "time": "13:30",
                    "timeStr": "13:30-14:00",
                    "datetime": "2022-08-28 13:30",
                    "date": 1661664652000
                },
                {
                    "cnDay": "周日",
                    "cnDate": "明天",
                    "cnDateWeekDay": "明天(08-28 周日)",
                    "ymd": "2022-08-28",
                    "time": "14:30",
                    "timeStr": "14:30-15:00",
                    "datetime": "2022-08-28 14:30",
                    "date": 1661668252000
                },
                {
                    "cnDay": "周日",
                    "cnDate": "明天",
                    "cnDateWeekDay": "明天(08-28 周日)",
                    "ymd": "2022-08-28",
                    "time": "15:30",
                    "timeStr": "15:30-16:00",
                    "datetime": "2022-08-28 15:30",
                    "date": 1661671852000
                },
                {
                    "cnDay": "周日",
                    "cnDate": "明天",
                    "cnDateWeekDay": "明天(08-28 周日)",
                    "ymd": "2022-08-28",
                    "time": "16:30",
                    "timeStr": "16:30-17:00",
                    "datetime": "2022-08-28 16:30",
                    "date": 1661675452000
                },
                {
                    "cnDay": "周日",
                    "cnDate": "明天",
                    "cnDateWeekDay": "明天(08-28 周日)",
                    "ymd": "2022-08-28",
                    "time": "17:30",
                    "timeStr": "17:30-18:00",
                    "datetime": "2022-08-28 17:30",
                    "date": 1661679052000
                },
                {
                    "cnDay": "周日",
                    "cnDate": "明天",
                    "cnDateWeekDay": "明天(08-28 周日)",
                    "ymd": "2022-08-28",
                    "time": "18:30",
                    "timeStr": "18:30-19:00",
                    "datetime": "2022-08-28 18:30",
                    "date": 1661682652000
                },
                {
                    "cnDay": "周日",
                    "cnDate": "明天",
                    "cnDateWeekDay": "明天(08-28 周日)",
                    "ymd": "2022-08-28",
                    "time": "19:30",
                    "timeStr": "19:30-20:00",
                    "datetime": "2022-08-28 19:30",
                    "date": 1661686252000
                },
                {
                    "cnDay": "周日",
                    "cnDate": "明天",
                    "cnDateWeekDay": "明天(08-28 周日)",
                    "ymd": "2022-08-28",
                    "time": "20:30",
                    "timeStr": "20:30-21:00",
                    "datetime": "2022-08-28 20:30",
                    "date": 1661689852000
                },
                {
                    "cnDay": "周日",
                    "cnDate": "明天",
                    "cnDateWeekDay": "明天(08-28 周日)",
                    "ymd": "2022-08-28",
                    "time": "21:30",
                    "timeStr": "21:30-22:00",
                    "datetime": "2022-08-28 21:30",
                    "date": 1661693452000
                },
                {
                    "cnDay": "周日",
                    "cnDate": "明天",
                    "cnDateWeekDay": "明天(08-28 周日)",
                    "ymd": "2022-08-28",
                    "time": "22:30",
                    "timeStr": "22:30-23:00",
                    "datetime": "2022-08-28 22:30",
                    "date": 1661697052000
                }
            ]
        },
        {
            "cnDateWeekDay": "后天(08-29 周一)",
            "datetime": "2022-08-29 07:30",
            "cnDate": "后天",
            "ymd": "2022-08-29",
            "list": [
                {
                    "cnDay": "周一",
                    "cnDate": "后天",
                    "cnDateWeekDay": "后天(08-29 周一)",
                    "ymd": "2022-08-29",
                    "time": "07:30",
                    "timeStr": "07:30-08:00",
                    "datetime": "2022-08-29 07:30",
                    "date": 1661729452000
                },
                {
                    "cnDay": "周一",
                    "cnDate": "后天",
                    "cnDateWeekDay": "后天(08-29 周一)",
                    "ymd": "2022-08-29",
                    "time": "08:30",
                    "timeStr": "08:30-09:00",
                    "datetime": "2022-08-29 08:30",
                    "date": 1661733052000
                },
                {
                    "cnDay": "周一",
                    "cnDate": "后天",
                    "cnDateWeekDay": "后天(08-29 周一)",
                    "ymd": "2022-08-29",
                    "time": "09:30",
                    "timeStr": "09:30-10:00",
                    "datetime": "2022-08-29 09:30",
                    "date": 1661736652000
                },
                {
                    "cnDay": "周一",
                    "cnDate": "后天",
                    "cnDateWeekDay": "后天(08-29 周一)",
                    "ymd": "2022-08-29",
                    "time": "10:30",
                    "timeStr": "10:30-11:00",
                    "datetime": "2022-08-29 10:30",
                    "date": 1661740252000
                },
                {
                    "cnDay": "周一",
                    "cnDate": "后天",
                    "cnDateWeekDay": "后天(08-29 周一)",
                    "ymd": "2022-08-29",
                    "time": "11:30",
                    "timeStr": "11:30-12:00",
                    "datetime": "2022-08-29 11:30",
                    "date": 1661743852000
                },
                {
                    "cnDay": "周一",
                    "cnDate": "后天",
                    "cnDateWeekDay": "后天(08-29 周一)",
                    "ymd": "2022-08-29",
                    "time": "12:30",
                    "timeStr": "12:30-13:00",
                    "datetime": "2022-08-29 12:30",
                    "date": 1661747452000
                },
                {
                    "cnDay": "周一",
                    "cnDate": "后天",
                    "cnDateWeekDay": "后天(08-29 周一)",
                    "ymd": "2022-08-29",
                    "time": "13:30",
                    "timeStr": "13:30-14:00",
                    "datetime": "2022-08-29 13:30",
                    "date": 1661751052000
                },
                {
                    "cnDay": "周一",
                    "cnDate": "后天",
                    "cnDateWeekDay": "后天(08-29 周一)",
                    "ymd": "2022-08-29",
                    "time": "14:30",
                    "timeStr": "14:30-15:00",
                    "datetime": "2022-08-29 14:30",
                    "date": 1661754652000
                },
                {
                    "cnDay": "周一",
                    "cnDate": "后天",
                    "cnDateWeekDay": "后天(08-29 周一)",
                    "ymd": "2022-08-29",
                    "time": "15:30",
                    "timeStr": "15:30-16:00",
                    "datetime": "2022-08-29 15:30",
                    "date": 1661758252000
                },
                {
                    "cnDay": "周一",
                    "cnDate": "后天",
                    "cnDateWeekDay": "后天(08-29 周一)",
                    "ymd": "2022-08-29",
                    "time": "16:30",
                    "timeStr": "16:30-17:00",
                    "datetime": "2022-08-29 16:30",
                    "date": 1661761852000
                },
                {
                    "cnDay": "周一",
                    "cnDate": "后天",
                    "cnDateWeekDay": "后天(08-29 周一)",
                    "ymd": "2022-08-29",
                    "time": "17:30",
                    "timeStr": "17:30-18:00",
                    "datetime": "2022-08-29 17:30",
                    "date": 1661765452000
                },
                {
                    "cnDay": "周一",
                    "cnDate": "后天",
                    "cnDateWeekDay": "后天(08-29 周一)",
                    "ymd": "2022-08-29",
                    "time": "18:30",
                    "timeStr": "18:30-19:00",
                    "datetime": "2022-08-29 18:30",
                    "date": 1661769052000
                }
            ]
        }
    ]
}`
            that = this;
            that.simpleCart.dateWeekDeliveryTimeList = JSON.parse(s).dateWeekDeliveryTimeList

        },
        methods: {
            openChooseTime() {
                this.showChooseTime = true;
            },
            closeChooseTime() {
                this.showChooseTime = false;
            },
            chooseTimeResult(dayIndex, hourIndex) {
                var result = this.simpleCart.dateWeekDeliveryTimeList[dayIndex]
                if (dayIndex == 0 && hourIndex == 0) {
                    that.dateStr = result.list[hourIndex].timeStr
                } else {
                    that.dateStr = result.cnDateWeekDay + result.list[hourIndex].timeStr
                }
                console.log(this.dateStr);
                that.datetime = result.list[hourIndex].datetime
                console.log(dayIndex + "--" + hourIndex)
            },
        }
    }
</script>

<style>
    .content {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    .logo {
        height: 200 rpx;
        width: 200 rpx;
        margin-top: 200 rpx;
        margin-left: auto;
        margin-right: auto;
        margin-bottom: 50 rpx;
    }

    .text-area {
        display: flex;
        justify-content: center;
    }

    .title {
        font-size: 36 rpx;
        color: #8f8f94;
    }
</style>
