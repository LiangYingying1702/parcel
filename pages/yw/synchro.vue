<template>
	<view class="content">
		<view >
			<button @click="fn" class="buttons">数据采集</button>
		</view>
		<view>今天同步了{{arr.length}}次</view>
		<view>
			<uni-badge v-for="obj in arr" :text="obj" type="primary" ></uni-badge>
		</view>
	</view>
</template>

<script>
	import uniBadge from "@dcloudio/uni-ui/lib/uni-badge/uni-badge.vue"
	export default {
		 components: {uniBadge},
		data() {
			return {
				arr:[],
				title:'hello'
			}
		},
		mounted() {
			uni.getStorage({
				key:"synchro",
				success:(res)=>{
					this.arr=res.data
				}
			})
		},
		methods:{
			fn(){
				var date = new Date();
				var cdate = date.getHours()+":"+date.getMinutes();
				this.arr.push("同步时间"+cdate);
				uni.setStorage({
					key:'synchro',
					data:this.arr
				})
			
			uni.getStorage({
				key:'baseUser',
				success:(res)=>{
					var compid = res.data.compid;
			uni.request({
				url:this.url+'produceReport/initCurrentDay?compid='+compid,
				data:{},
				header:{
					'custom-header':'hello'
				},
				success:(res)=>{
					uni.showToast({
						title:'采集成功'
						})
					}
				})
			}
		})
			
			}
		}
	}
</script>

<style>
	
</style>
