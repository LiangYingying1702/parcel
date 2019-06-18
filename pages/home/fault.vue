<template>
	<view class="content">
		<view>
			<picker @change="fn1" :value="index" :range="arr" range-key="devname">
				<view class="uni-input">{{arr[index].devname}}</view>
			</picker>
			<input class="input" type="text" v-model="cause" placeholder="请输入故障原因"></input>
			<input class="input" type="text" v-model="faultuser" placeholder="请输入报修人"></input>
			<input class="input" type="text" v-model="faulttime" placeholder="请输入故障时间"></input>
			<button @click="fn2" class="buttons">提交</button>
		</view>
		
	</view>
</template>

<script>
	import uniIcon from "@dcloudio/uni-ui/lib/uni-icon/uni-icon.vue"
	export default {
		components: {uniIcon},
		data() {
			return {
				devid:'',
				devname:'',
				fault_id:'',
				cause:'',
				faultuser:'',
				faulttime:'',
				arr:[{devname:''}],
				index:0
			}
		},
		mounted() {
			uni.request({
				url: this.url + 'baseDevice/list',
				header: {
					'custom-header': 'fault'
				},
				success: (res) => {
					this.arr = res.data;
				}
			})
		},
		methods:{
			fn1(e){
				this.index = e.target.value;
			},
			fn2(){
				if (this.cause.length <= 0) {
					uni.showToast({
						icon: 'none',
						title: '请输入故障原因',
						duration: 1000
					});
					return;
				}
				if (this.faultuser.length <= 0) {
					uni.showToast({
						icon: 'none',
						title: '请输入报修人',
						duration: 1000
					});
					return;
				}
				if (this.faulttime.length <= 0) {
					uni.showToast({
						icon: 'none',
						title: '请输入报修时间',
						duration: 1000
					});
					return;
				}
				//网络请求
				uni.request({
					url: this.url + 'produceFault/insert',
					data: {
						devid: this.arr[this.index].devid,
						devname: this.devname,
						cause: this.cause,
						faultuser: this.faultuser,
						faulttime: this.faulttime
					},
					header: {
						'custom-header': 'fault'
					},
					success: (res) => {
						uni.showToast({
							icon: 'success',
							title: '提交成功',
							duration: 1000
						});
						uni.redirectTo({
							url: 'login'
						});
					},
					fail: (res) => {
						uni.showToast({
							icon: 'none',
							title: '网络异常,请稍后重试',
							duration: 1000
						});
					},
					
				})
			}
		}
	}
</script>

<style>
	@import url("../../static/css/fault.css");
</style>
