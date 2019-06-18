<template>
	<view class="content">
		<view>
			<text class="title">港口能耗排名</text>
			<table01></table01>
		</view>
	</view>
</template>

<script>
	import table01 from "../tables/table01.vue"
	export default {
		components: {
			table01
		},
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style>
	
</style>
