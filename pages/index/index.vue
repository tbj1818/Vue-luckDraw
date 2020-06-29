<template>
	<view class="content">
		<view class="logo">
			<img src="@/static/images/logo.png" />
		</view>
		<view class="main">
			<view class="activity-amin2">
				<input type="text" class="phoneinput" v-model="realname" placeholder="请输入姓名" />
				<input type="text" class="phoneinput" v-model="phone" maxlength="11" placeholder="请输入手机账号" />
				<input type="text" class="phoneinput" v-model="company" placeholder="请输入公司姓名" />
				<view class="prompt1"></view>
				<button class="wt1 wt4" @click="submit">提交并抽奖</button>
			</view>
			<view class="text-main">
				<h1> 活动规则</h1>
				<p>1.活动时间：2018年10月18日——2018年12月31日。<br />
					2.本次活动为福建某某公司专属特权活动，仅针对目标用户参与。<br />
					3.活动期间，福建某某公司专属客户每天可参与抽奖一次。<br />
					4.每天分享到朋友圈还可以参加博饼一次。<br />
				</p>
			</view>

		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				realname: '',
				phone: '',
				company: '',
				successdialog: false,
				prize: '谢谢参与'
			}
		},
		onLoad() {

		},
		methods: {
			submit() {
				if (!this.realname) {
					uni.showToast({
						title: '请输入姓名',
						icon: 'none',
						duration: 2000
					});
				} else
				if (!this.phone) {
					uni.showToast({
						title: '请输入手机号',
						icon: 'none',
						duration: 2000
					});
				} else
				if (!this.company) {
					uni.showToast({
						title: '请输入公司姓名',
						icon: 'none',
						duration: 2000
					});
				} else {
					uni.navigateTo({
						url: '/pages/index/draw'
					});
					// this.successdialog=true
					// this.prize='iphone12一部'
				}
			},
			hidedialog() {
				this.successdialog = false
			}
		}
	}
</script>

<style>

</style>
