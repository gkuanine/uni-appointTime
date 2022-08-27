<template>
	<view style="display:flex;flex-direction:column;">
		<view style="display:flex;flex-direction:row;justify-content:center; height:45px;text-align:center;line-height:45px;" @click="openChooseTime">{{datetime==''?"选择时间":dateStr}}</view>
		<appointTime v-on:closeChooseTime="closeChooseTime" v-on:chooseTimeResult="chooseTimeResult"
				 v-show="showChooseTime"  style="height:100%; position:fixed;bottom:0px;left:0px;" ref="appointTime"
				 :timeList="simpleCart.dateWeekDeliveryTimeList" :datetime="datetime"></appointTime>
	</view>
</template>

<script>
	import appointTime from '../../components/appointTime.vue'
	var that ;
	export default {
		components: {
				appointTime
		},
		data() {
			return {
				title: 'Hello',
				datetime:"",
				dateStr:"",
				showChooseTime:false,
				//购物车数据
								simpleCart: {
									allCart:[],
									cartTotal:{
										checked: 0,
										checkedProductAmount: 0,
										checkedProductCount: 0,
										productAmount: "0.00",
										productCount: 0
									},
									timeList:{},
									dateWeekDeliveryTimeList:[]
								},
			}
		},
		onLoad() {
			var s = `{"code":200,"data":{"allCart":[{"shopName":"","shopCode":"","shopValidPrice":0,"shopId":1,"shopIcon":null,"updateTime":"","checked":1,"inValid":0,"cartList":[{"id":162,"version":0,"createdAt":"2022-08-19 18:39:18","updatedAt":"2022-08-25 18:59:21","deletedAt":null,"createdBy":0,"updatedBy":0,"nameSuffix":"33","userId":1,"productId":4,"skuId":34,"buyNum":1,"checked":1,"addPrice":"20.02","shareId":0,"staffId":0,"shopId":1,"stock":4,"maxBuy":100,"minBuy":0,"hasBuy":0,"remarks":"","productSn":"","batchId":0,"onSale":1,"salesPrice":"20.02","diffPrice":"0","pic":"https://qiniu.linjiangping.com/test/nidemall/20211212091509kt007.png","title":"散装普洱茶 500g","batchVersion":0,"batchStock":0,"skuStock":0,"skuVersion":0,"status":0},{"id":161,"version":0,"createdAt":"2022-08-18 20:54:08","updatedAt":"2022-08-27 13:38:43","deletedAt":null,"createdBy":0,"updatedBy":0,"nameSuffix":"33","userId":1,"productId":4,"skuId":35,"buyNum":2,"checked":1,"addPrice":"10.01","shareId":0,"staffId":0,"shopId":1,"stock":14,"maxBuy":100,"minBuy":0,"hasBuy":0,"remarks":"","productSn":"","batchId":0,"onSale":1,"salesPrice":"10.01","diffPrice":"0","pic":"https://qiniu.linjiangping.com/test/nidemall/20211212091518kt3.png","title":"散装普洱茶 200g","batchVersion":0,"batchStock":0,"skuStock":0,"skuVersion":0,"status":0}]}],"cartTotal":{"productCount":3,"checkedProductCount":3,"checkedProductAmount":"40.04","productAmount":"40.04","checked":1,"canUseCouponList":null,"canNotUseCouponList":null},"dateWeekDeliveryTimeList":[{"cnDateWeekDay":"今天(08-27 周六)","datetime":"2022-08-27 14:37","cnDate":"今天","ymd":"2022-08-27","list":[{"cnDay":"周六","cnDate":"今天","cnDateWeekDay":"今天(08-27 周六)","ymd":"2022-08-27","time":"立即送出","timeStr":"立即送出","datetime":"2022-08-27 14:37","date":1661582278390},{"cnDay":"周六","cnDate":"今天","cnDateWeekDay":"今天(08-27 周六)","ymd":"2022-08-27","time":"15:00","timeStr":"15:00-15:30","datetime":"2022-08-27 15:00","date":1661583658000},{"cnDay":"周六","cnDate":"今天","cnDateWeekDay":"今天(08-27 周六)","ymd":"2022-08-27","time":"15:30","timeStr":"15:30-16:00","datetime":"2022-08-27 15:30","date":1661585458000},{"cnDay":"周六","cnDate":"今天","cnDateWeekDay":"今天(08-27 周六)","ymd":"2022-08-27","time":"16:30","timeStr":"16:30-17:00","datetime":"2022-08-27 16:30","date":1661589058000},{"cnDay":"周六","cnDate":"今天","cnDateWeekDay":"今天(08-27 周六)","ymd":"2022-08-27","time":"17:30","timeStr":"17:30-18:00","datetime":"2022-08-27 17:30","date":1661592658000},{"cnDay":"周六","cnDate":"今天","cnDateWeekDay":"今天(08-27 周六)","ymd":"2022-08-27","time":"18:30","timeStr":"18:30-19:00","datetime":"2022-08-27 18:30","date":1661596258000},{"cnDay":"周六","cnDate":"今天","cnDateWeekDay":"今天(08-27 周六)","ymd":"2022-08-27","time":"19:30","timeStr":"19:30-20:00","datetime":"2022-08-27 19:30","date":1661599858000},{"cnDay":"周六","cnDate":"今天","cnDateWeekDay":"今天(08-27 周六)","ymd":"2022-08-27","time":"20:30","timeStr":"20:30-21:00","datetime":"2022-08-27 20:30","date":1661603458000},{"cnDay":"周六","cnDate":"今天","cnDateWeekDay":"今天(08-27 周六)","ymd":"2022-08-27","time":"21:30","timeStr":"21:30-22:00","datetime":"2022-08-27 21:30","date":1661607058000},{"cnDay":"周六","cnDate":"今天","cnDateWeekDay":"今天(08-27 周六)","ymd":"2022-08-27","time":"22:30","timeStr":"22:30-23:00","datetime":"2022-08-27 22:30","date":1661610658000}]},{"cnDateWeekDay":"明天(08-28 周日)","datetime":"2022-08-28 07:30","cnDate":"明天","ymd":"2022-08-28","list":[{"cnDay":"周日","cnDate":"明天","cnDateWeekDay":"明天(08-28 周日)","ymd":"2022-08-28","time":"07:30","timeStr":"07:30-08:00","datetime":"2022-08-28 07:30","date":1661643058000},{"cnDay":"周日","cnDate":"明天","cnDateWeekDay":"明天(08-28 周日)","ymd":"2022-08-28","time":"08:30","timeStr":"08:30-09:00","datetime":"2022-08-28 08:30","date":1661646658000},{"cnDay":"周日","cnDate":"明天","cnDateWeekDay":"明天(08-28 周日)","ymd":"2022-08-28","time":"09:30","timeStr":"09:30-10:00","datetime":"2022-08-28 09:30","date":1661650258000},{"cnDay":"周日","cnDate":"明天","cnDateWeekDay":"明天(08-28 周日)","ymd":"2022-08-28","time":"10:30","timeStr":"10:30-11:00","datetime":"2022-08-28 10:30","date":1661653858000},{"cnDay":"周日","cnDate":"明天","cnDateWeekDay":"明天(08-28 周日)","ymd":"2022-08-28","time":"11:30","timeStr":"11:30-12:00","datetime":"2022-08-28 11:30","date":1661657458000},{"cnDay":"周日","cnDate":"明天","cnDateWeekDay":"明天(08-28 周日)","ymd":"2022-08-28","time":"12:30","timeStr":"12:30-13:00","datetime":"2022-08-28 12:30","date":1661661058000},{"cnDay":"周日","cnDate":"明天","cnDateWeekDay":"明天(08-28 周日)","ymd":"2022-08-28","time":"13:30","timeStr":"13:30-14:00","datetime":"2022-08-28 13:30","date":1661664658000},{"cnDay":"周日","cnDate":"明天","cnDateWeekDay":"明天(08-28 周日)","ymd":"2022-08-28","time":"14:30","timeStr":"14:30-15:00","datetime":"2022-08-28 14:30","date":1661668258000},{"cnDay":"周日","cnDate":"明天","cnDateWeekDay":"明天(08-28 周日)","ymd":"2022-08-28","time":"15:30","timeStr":"15:30-16:00","datetime":"2022-08-28 15:30","date":1661671858000},{"cnDay":"周日","cnDate":"明天","cnDateWeekDay":"明天(08-28 周日)","ymd":"2022-08-28","time":"16:30","timeStr":"16:30-17:00","datetime":"2022-08-28 16:30","date":1661675458000},{"cnDay":"周日","cnDate":"明天","cnDateWeekDay":"明天(08-28 周日)","ymd":"2022-08-28","time":"17:30","timeStr":"17:30-18:00","datetime":"2022-08-28 17:30","date":1661679058000},{"cnDay":"周日","cnDate":"明天","cnDateWeekDay":"明天(08-28 周日)","ymd":"2022-08-28","time":"18:30","timeStr":"18:30-19:00","datetime":"2022-08-28 18:30","date":1661682658000},{"cnDay":"周日","cnDate":"明天","cnDateWeekDay":"明天(08-28 周日)","ymd":"2022-08-28","time":"19:30","timeStr":"19:30-20:00","datetime":"2022-08-28 19:30","date":1661686258000},{"cnDay":"周日","cnDate":"明天","cnDateWeekDay":"明天(08-28 周日)","ymd":"2022-08-28","time":"20:30","timeStr":"20:30-21:00","datetime":"2022-08-28 20:30","date":1661689858000},{"cnDay":"周日","cnDate":"明天","cnDateWeekDay":"明天(08-28 周日)","ymd":"2022-08-28","time":"21:30","timeStr":"21:30-22:00","datetime":"2022-08-28 21:30","date":1661693458000},{"cnDay":"周日","cnDate":"明天","cnDateWeekDay":"明天(08-28 周日)","ymd":"2022-08-28","time":"22:30","timeStr":"22:30-23:00","datetime":"2022-08-28 22:30","date":1661697058000}]},{"cnDateWeekDay":"后天(08-29 周一)","datetime":"2022-08-29 07:30","cnDate":"后天","ymd":"2022-08-29","list":[{"cnDay":"周一","cnDate":"后天","cnDateWeekDay":"后天(08-29 周一)","ymd":"2022-08-29","time":"07:30","timeStr":"07:30-08:00","datetime":"2022-08-29 07:30","date":1661729458000},{"cnDay":"周一","cnDate":"后天","cnDateWeekDay":"后天(08-29 周一)","ymd":"2022-08-29","time":"08:30","timeStr":"08:30-09:00","datetime":"2022-08-29 08:30","date":1661733058000},{"cnDay":"周一","cnDate":"后天","cnDateWeekDay":"后天(08-29 周一)","ymd":"2022-08-29","time":"09:30","timeStr":"09:30-10:00","datetime":"2022-08-29 09:30","date":1661736658000},{"cnDay":"周一","cnDate":"后天","cnDateWeekDay":"后天(08-29 周一)","ymd":"2022-08-29","time":"10:30","timeStr":"10:30-11:00","datetime":"2022-08-29 10:30","date":1661740258000},{"cnDay":"周一","cnDate":"后天","cnDateWeekDay":"后天(08-29 周一)","ymd":"2022-08-29","time":"11:30","timeStr":"11:30-12:00","datetime":"2022-08-29 11:30","date":1661743858000},{"cnDay":"周一","cnDate":"后天","cnDateWeekDay":"后天(08-29 周一)","ymd":"2022-08-29","time":"12:30","timeStr":"12:30-13:00","datetime":"2022-08-29 12:30","date":1661747458000},{"cnDay":"周一","cnDate":"后天","cnDateWeekDay":"后天(08-29 周一)","ymd":"2022-08-29","time":"13:30","timeStr":"13:30-14:00","datetime":"2022-08-29 13:30","date":1661751058000},{"cnDay":"周一","cnDate":"后天","cnDateWeekDay":"后天(08-29 周一)","ymd":"2022-08-29","time":"14:30","timeStr":"14:30-15:00","datetime":"2022-08-29 14:30","date":1661754658000},{"cnDay":"周一","cnDate":"后天","cnDateWeekDay":"后天(08-29 周一)","ymd":"2022-08-29","time":"15:30","timeStr":"15:30-16:00","datetime":"2022-08-29 15:30","date":1661758258000},{"cnDay":"周一","cnDate":"后天","cnDateWeekDay":"后天(08-29 周一)","ymd":"2022-08-29","time":"16:30","timeStr":"16:30-17:00","datetime":"2022-08-29 16:30","date":1661761858000}]}],"imediaDeliveryTime":{"cnDay":"周六","cnDate":"今天","cnDateWeekDay":"今天(08-27 周六)","ymd":"2022-08-27","time":"立即送出","timeStr":"立即送出","datetime":"2022-08-27 14:37","date":1661582278390},"orderInfo":{"orderAmount":"40.04","couponAmount":"0","freightAmount":"0","packageAmount":"0","payAmount":"40.04"}},"msg":"操作成功"}`
			that = this;
			that.simpleCart = JSON.parse(s).data
			debugger
			console.log(that.simpleCart)
		},
		methods: {
		openChooseTime(){
				this.showChooseTime = true;
			},
			closeChooseTime(){
				this.showChooseTime = false;
			},
			chooseTimeResult(dayIndex,hourIndex){
				var result =  this.simpleCart.dateWeekDeliveryTimeList[dayIndex]
				if (dayIndex ==0 && hourIndex ==0){
					that.dateStr = 	result.list[hourIndex].timeStr
				}else {
					that.dateStr = result.cnDateWeekDay + result.list[hourIndex].timeStr
				}
				console.log(this.dateStr);
				that.datetime = result.list[hourIndex].datetime
				console.log(dayIndex+"--"+hourIndex)
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
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
