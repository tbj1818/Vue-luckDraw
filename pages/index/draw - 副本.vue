<template>
	<div id="rotary-table">
		<!-- <ul class="light clearfix">
			<li class="fl">
				<p></p>
				<p class="blin"></p>
				<p></p>
				<p class="blin"></p>
			</li>
			<li class="fr">
				<p class="blin"></p>
				<p></p>
				<p class="blin"></p>
				<p></p>
			</li>
		</ul> -->
		<div class="award" v-for="(award,index) in awards" :class="['award'+index,{'active': index==current}]">
			{{award.name}}
		</div>
		<div id="start-btn" @click="start"></div>
		<div class="main">
			<!--中奖提示-->
			<div id="mask" v-if="successdialog">
				<div class="blin"></div>

				<div id="share" class="winner" v-if="successdialog">
					<div class="winner-main">
						<h3 id="p1"></h3>
						<p>恭喜您获得了<p id="p2">{{prize}}</p>
						</p>
						<a href="#" class="but" id="but" @click="hidedialog">确定</a>
					</div>
				</div>
			</div>
			<!-- 中将弹窗 -->
		</div>
	</div>
</template>
<script>
	export default {
		name: 'raffle',
		data() {
			return {
				current: 0,
				awards: [{
						id: 1,
						name: '空'
					},
					{
						id: 2,
						name: '眼镜'
					},
					{
						id: 3,
						name: '包'
					},
					{
						id: 4,
						name: '谢谢'
					},
					{
						id: 5,
						name: '书'
					},
					{
						id: 6,
						name: '手链'
					},
					{
						id: 7,
						name: '美女'
					},
					{
						id: 8,
						name: 'iphone'
					}
				],
				speed: 200,
				diff: 15,
				award: {},
				successdialog: false,
				prize: '谢谢参与',
				time: 0
			};
		},
		methods: {
			start() {
				// 开始抽奖
				this.drawAward();
				this.time = Date.now();
				this.speed = 200;
				this.diff = 15;
			},
			drawAward() {
				// 请求接口, 这里我就模拟请求后的数据(请求时间为2s)
				setTimeout(() => {
					this.award = {
						id: '4',
						name: '笨驴',
					};
				}, 1000);
				this.move();
			},
			hidedialog() {
				this.successdialog = false
			},
			move() {
				window.timeout = setTimeout(() => {
					this.current++;
					if (this.current > 7) {
						this.current = 0;
					}
					if (this.award.id && (Date.now() - this.time) / 1000 > 2) {
						this.speed += this.diff;
						if ((Date.now() - this.time) / 1000 > 4 && this.award.id == this.awards[this.current].id) {
							clearTimeout(window.timeout);
							setTimeout(() => {
								// alert( '恭喜你，抽中了' + this.award.name );
								this.successdialog = true
								this.prize = this.prize
							}, 0);
							return;
						}
					} else {
						this.speed -= this.diff;
					}
					console.log(this.speed);
					this.move();
				}, this.speed);
			}
		}
	};
</script>

<style rel="stylesheet/less" lang="less">
	#rotary-table {
		width: 340px;
		height: 349px;
		position: relative;
		margin: auto;
		background-color: antiquewhite;
		border-radius: 15px;
		.award {
			width: 90px;
			height: 96px;
			line-height: 96px;
			text-align: center;
			float: left;
			position: absolute;
			overflow: hidden;
			background: url(../../static/images/normal.png) no-repeat center center;
			background-size: contain;

			// background-color: aquamarine;
			&.active {
				// background-color: darkgoldenrod;
				background: url(../../static/images/select.png) no-repeat center center;
				background-size: contain;
			}

			&.award0 {
				top: 21px;
				left: 21px;
			}

			&.award1 {
				top: 21px;
				left: 125px;
			}

			&.award2 {
				top: 21px;
				right: 22px;
			}

			&.award3 {
				top: 126px;
				right: 22px;
			}

			&.award4 {
				bottom: 22.5px;
				right: 22px;
			}

			&.award5 {
				bottom: 22.5px;
				right: 125.5px;
			}

			&.award6 {
				bottom: 22.5px;
				left: 21px;
			}

			&.award7 {
				top: 126px;
				left: 21px;
			}
		}

		#start-btn {
			position: absolute;
			background: url(../../static/images/start.png) no-repeat center center;
			background-size: contain;
			top: 125px;
			left: 124px;
			width: 90px;
			height: 96px;
			line-height: 90px;
			text-align: center;

		}
	}
</style>
