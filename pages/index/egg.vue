<template>
	<div class="lottery-box">
		<div class="zjd2">
			<div class="common">
				<div class="right_prize" @click="linkhistory"><img src="//cdn.choujiangle.cn/themes/common/prize.png"></div>
			</div>
			<div class="header"><img src="//cdn.choujiangle.cn/themes/zjd2/title.png"></div>
			<div class="shan"><img src="//cdn.choujiangle.cn/themes/zjd/guang.png"></div>
			<div class="main" @click="startLottery">
				<div class="zd_chuizi">
					<img src="/static/images/zd_cion01.png">
				</div>
				<div class="eggs" >
					<div class="egg_content hitEgg_rotate">
						<div class="egg_1 egg1"><img src="//cdn.choujiangle.cn/themes/zjd2/egg.png" class="egg_rottate img1"></div>
						<div class="egg_1 egg2"><img src="//cdn.choujiangle.cn/themes/zjd2/egg.png" class="egg_rottate img1"></div>
						<div class="egg_1 egg3"><img src="//cdn.choujiangle.cn/themes/zjd2/egg.png" class="egg_rottate img1"></div>
					</div>
				</div>
				<div class="di"><img src="//cdn.choujiangle.cn/themes/zjd2/stage.png"></div>
			</div>
			<div class="hide" style="display: none;"><img width="150" src="//cdn.choujiangle.cn/themes/zjd2/broke1.png" class="broke"></div>
			<div class="draw_time">
				您还有 1 次机会
			</div>
			<div class="egg_footer">
				<div class="introduction">
					<div class="zbf">
						<div class="toubu">
							活动规则
						</div>
						<div class="text">
							<p>易临抽奖易临抽奖易临抽奖易临抽奖易临抽奖易临抽奖</p>
						</div>
					</div>
				</div>
				<view class="history" @click="linkhistory">中奖历史</view>
			</div>
		</div>
		<!-- 中奖弹窗 -->
		<div class="mask" v-if="showToast">
			<div class="blin"></div>
		</div>
		<div class="lottery-alert" v-if="showToast">
			<h1>恭喜您</h1>
			<p><img src="/static/images/j2.png" alt=""></p>
			<h2>获得大奖</h2>
			<div class="btnsave" @click="showToast=false">确定</div>
		</div>
	</div>
</template>
<script>
	export default {
		name: 'raffle',
		data() {
			return {
				 drawnum:2,
				 showToast:false
			};
		},
		methods: {
			startLottery() {
				console.log(this.drawnum)
				if (this.drawnum > 0) {
					this.startRoll();
				} else {
					uni.showToast({
						title: '剩余次数不足',
						icon: 'none',
						duration: 2000
					});
					return
				}
				this.drawnum--
			},
			// 开始转动
			startRoll() {
				var that=this
					setTimeout(res => {
						that.showToast = true;
					}, 500)
			},
			linkhistory() {
				uni.navigateTo({
					url: '/pages/index/history'
				});
			}
		}
	};
</script>
