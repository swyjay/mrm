<template>
	<div class="suvery-box">
		<div class='suvery-count'>{{sale.count | commaSepNumber}}<span>箱</span></div>
		<div class='suvery-more' :class="sale.state">
			<div class='change-count'>
				{{sale.change}}箱
				<i class='fa' :class="{'fa-arrow-down': sale.state==='down','fa-arrow-up': sale.state==='up'}"></i>
			</div>
			<div class='change-rate'>
				{{sale.rate}}
				<i class='fa' :class="{'fa-arrow-down': sale.state==='down','fa-arrow-up': sale.state==='up'}"></i>
			</div>
		</div>
		<div class='saleCountChart' ref="suverySaleChart">
		</div>
	</div>
</template>
<script>
import axios from 'axios'
import echarts from 'echarts'
export default {
	props: {
		sourcekey: String
	},
	data() {
		return {
			sale: {
				count: '15953',
				change: '953',
				rate: '1.30%',
				state: 'down'
			}
		}
	},
	mounted() {
		this.initChart();
	},
	methods: {
		initChart() {
			let myChart = echarts.init(this.$refs.suverySaleChart);
			myChart.setOption(this.getChartOption());
		},
		getChartOption() {
			var dataObj = this.getChartData();
					var option = {
						tooltip: {
							show: false
						},
						barWidth: "25px",
						grid: {
							left: '0px',
							containLabel: true,
							bottom: '10px',
							top: '20px'
						},
						xAxis: {
							axisLine: { //横坐标线是否显示
								show: false
							},
							axisTick: {
								show: false
							},
							type: 'category',
							nameTextStyle: {
								fontSize: '1rem',
								fontFamily: 'inhert',
							},
							boundaryGap: false,
							data: dataObj.year
						},
						yAxis: {
							show: false,
							min: 0
						},
						textStyle: {
							color: '#999999'
						},
						series: [{
							type: 'bar',
							stack: '总量',
							symbolSize: 10,
							color: '#ff9966',
							itemStyle: {
								normal: {
									borderColor: '#ff9966',
									color: '#ff9966'
								}
							},
							label: {
				            		normal: {
				            			show: true,
				            			position: 'top',
				            			formatter: '{c}'+'万箱',
				            			textStyle: {
				            				color: '#ff9966'
				            			}
				            		}
				            },
							data: dataObj.data
						}]
					}
				return option;
		},
		getChartData() {
				var random = function (min,max) {
				    return Math.floor(Math.random()*(max-min+1)+min);
				};
				var year = ['2012年','2013年','2014年','2015年','2016年'];
				var data = [];
				if(this.sourcekey == "china"){
					for(var i=0;i<5;i++){
						data.push(random(3000,4500));
					}
				}else{
					for(var i=0;i<5;i++){
						data.push(random(150,250));
					}
				}

				return {
					year:year,
					data:data
				}
		}
	}
}
</script>
<style>

</style>
