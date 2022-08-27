<template>
    <view class="appoint-time">
        <view style="width:100%;height:55%;background:black;opacity: 0.5;"></view>
        <view style="width:100%;height:45%;background:white;border-radius: 35px 35px 0px 0px">
        <view style="display:flex;flex-direction:row-reverse;justify-content:center;">
            <view style="height:45px;width:45px;color:red;fontsize:35px;text-align:center;line-height:45px;" @click="closeChooseTime">x</view><view style="width:100%;text-align:center;line-height:45px;" >选择预约时间</view>
        </view>
          <view style="display:flex;flex-direction:row;">
              <view style="display:flex;flex-direction:column;width:30%;background:white">
                  <view style="width:100%;display:flex;justify-content:center;" v-for="(item,index) in days">
                      <text style="text-align:center;line-height:45px;width:100%;background:#dedada" @click="dayIndexClick(index)" v-if="dayIndex==index">{{item}}</text>
                      <text style="text-align:center;line-height:45px;width:100%;background:white" @click="dayIndexClick(index)" v-if="dayIndex!=index">{{item}}</text>
                  </view>
              </view>
              <view style="width:1px;height:100%;background:#dedada">  </view>

              <scroll-view style="display:flex;flex-direction:column;width:70%;height:100%;">
                  <view style="width:100%;display:flex;justify-content:center;" v-for="(item,index) in dataTimeList[dayIndex]">
                      <text style="text-align:center;line-height:40px;width:100%;color:red" @click="hourIndexClick(index)" v-if="hourIndex==index">{{item.timeStr}}👈🏻</text>
                      <text style="text-align:center;line-height:45px;width:100%;" @click="hourIndexClick(index)" v-if="hourIndex!=index">{{item.timeStr}}</text>
                  </view>
              </scroll-view>
          </view>
        </view>
    </view>
</template>

<script>
    var that ;
    export default {
        name: 'appointTime',
        props: {
            timeList:{}
        },
        watch: {
            timeList:{
                handler(new__, old__) {
                    if (new__.length>0) {
                        that.initTimeData();
                    }
                },
                immediate: true,
                deep: true
            }
        },
        data() {
            return {
                showChooseTime:false,
                //全选
                days:[],
                datetime:"",
                dayIndex:0,
                hourIndex:0,
                dataTimeList:[],

            }
        },
        mounted() {
            that = this;
            console.log(this.timeList)
            console.log(this.days)
            that.initTimeData()
            setTimeout(() => {
                that.dayIndexClick(0)
            },100)

        },
        onLoad() {
            that = this;


            console.log(this.timeList)
        },
        beforeUpdate(){
            console.log('数据发生变化');
        },
        updated(){
            console.log('数据渲染完成');

        },

        methods: {
            initTimeData(){
                console.log("initTimeData")
                that.days = []
                that.dataTimeList =[]

                if (this.timeList) {
                    for (var i = 0; i < this.timeList.length; i++) {
                        var item = this.timeList[i];
                        that.days = that.days.concat(item.cnDate)
                        that.dataTimeList.push(item.list)
                    }

                }
                console.log(that.dataTimeList)
            },
            dayIndexClick(index){
                this.dayIndex = index
                this.hourIndex = 0
                this.$emit('chooseTimeResult', this.dayIndex,this.hourIndex)
            },
            hourIndexClick(index){
                this.hourIndex = index
                this.$emit('chooseTimeResult', this.dayIndex,this.hourIndex)
            },
            closeChooseTime(){
                this.$emit('closeChooseTime')
            },
        }
    };
</script>

<style>

.appoint-time{
    position:fixed;
    bottom:0px;left:0px;
    width:100%;
    height:40%;

}

</style>
