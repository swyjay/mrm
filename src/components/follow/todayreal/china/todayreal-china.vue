<template>
<div class="container">
  <mt-header fixed title="全国">
    <router-link to="/follow" slot="left">
      <mt-button icon="back">返回</mt-button>
    </router-link>
  </mt-header>
  <section class='todayreal'>
    <div class="order-count">
      <span class="name">今日实时订单数</span>
      <span class="value">
  				<animatedInteger v-bind:value="realTimeData.orderCount"></animatedInteger><span class="unit">笔</span>
      </span>
      <canvas ref="canvas"></canvas>
    </div>
    <div class="bottom-box">
      <div class="left">
        <span class="name">今日实时订购量</span>
        <span class="value">
  					<animatedInteger v-bind:value="realTimeData.orderAmount"></animatedInteger><span class="unit">箱</span>
        </span>
      </div>
      <div class="right">
        <span class="name">今日实时订单金额</span>
        <span class="value">
  					<animatedInteger v-bind:value="realTimeData.orderMoney"></animatedInteger><span class="unit">万元</span>
        </span>
      </div>
    </div>
  </section>
  <table-box title="今日各省实时销售情况" unit="单位：笔、条">
    <el-table :data="tableData" stripe style="width: 100%" :default-sort = "{prop: 'count', order: 'descending'}">
      <el-table-column prop="province" sortable label="省份"></el-table-column>
      <el-table-column prop="count" sortable label="订单笔数"></el-table-column>
      <el-table-column prop="amount" sortable label="订单量"></el-table-column>
    </el-table>
  </table-box>
</div>
</template>

<script>
import tableBox from 'components/follow/box/table-box'
import animatedInteger from 'components/follow/todayreal/animated-integer'
import {Table, TableColumn} from 'element-ui'

var random = function(min, max) {
  return Math.floor(Math.random() * (max - min + 1) + min);
};

export default {
  props: {
    city: Object,
    swiperIndex: Number
  },
  data() {
    return {
      realTimeData: {
        "orderCount": 1035,
        "orderAmount": 1052,
        "orderMoney": 619
      },
      timer: 0,
      tableData: [{
          province: '河南',
          count: random(10, 300),
          amount: random(1000, 10000)
        },
        {
          province: '辽宁',
          count: random(10, 300),
          amount: random(1000, 10000)
        },
        {
          province: '江西',
          count: random(10, 300),
          amount: random(1000, 10000)
        },
        {
          province: '西藏',
          count: random(10, 300),
          amount: random(1000, 10000)
        },
        {
          province: '吉林',
          count: random(10, 300),
          amount: random(1000, 10000)
        },
        {
          province: '黑龙江',
          count: random(10, 300),
          amount: random(1000, 10000)
        },
        {
          province: '广西',
          count: random(10, 300),
          amount: random(1000, 10000)
        },
        {
          province: '四川',
          count: random(10, 300),
          amount: random(1000, 10000)
        },
        {
          province: '浙江',
          count: random(10, 300),
          amount: random(1000, 10000)
        },
        {
          province: '江苏',
          count: random(10, 300),
          amount: random(1000, 10000)
        },
        {
          province: '北京',
          count: random(10, 300),
          amount: random(1000, 10000)
        },
        {
          province: '海南岛',
          count: random(10, 300),
          amount: random(1000, 10000)
        },
        {
          province: '陕西',
          count: random(10, 300),
          amount: random(1000, 10000)
        },
        {
          province: '宁夏',
          count: random(10, 300),
          amount: random(1000, 10000)
        },
        {
          province: '湖北',
          count: random(10, 300),
          amount: random(1000, 10000)
        },
        {
          province: '广东',
          count: random(10, 300),
          amount: random(1000, 10000)
        }
      ]
    }
  },
  components: {
    'table-box':tableBox,
    animatedInteger,
    "el-table":Table,
    "el-table-column":TableColumn
  },
  methods: {
    getRealTimeData: function() {
      this.timer = setInterval(() =>
        this.realTimeData = {
          "orderCount": this.realTimeData.orderCount + random(1, 10),
          "orderAmount": this.realTimeData.orderAmount + random(1, 3),
          "orderMoney": this.realTimeData.orderMoney + random(1, 3)
        }, 3000);
    }
  },
  mounted: function() {
    this.getRealTimeData();
    document.body.scrollTop = 0
  }
}
</script>
<style lang='stylus' scoped>
.container
  padding-top 40px
  background #eee
  .mint-header
    background #ffffff
    color #333333
    .mint-button
      color #26a2ff
  .todayreal
  	background #ffffff
  	margin-bottom 10px
  	.order-count
  		background #26a2ff
  		padding-bottom 20px
  		padding-top 20px
  		position relative
  		.name
  			display block
  			text-align center
  			color #ffffff
  			font-size 12px
  		.value
  			display block
  			text-align center
  			font-size 48px
  			color #ffffff
  			margin-top 10px
  			font-weight bold
  			.unit
  				font-size 24px
  		.button-container
  			display block
  			margin-top 15px
  			text-align center
  			.mint-button--default.is-plain
  				border-color #ffffff
  				color #ffffff
  				z-index 999
  		canvas
  			position absolute
  			width 100%
  			height 100%
  			top 0
  			left 0
  			z-index 0
  	.bottom-box
  		border-top #ccc 1px solid
  		display flex
  		padding-bottom 10px
  		.left
  			flex 1
  			.name
  				display block
  				margin-top 15px
  				text-align center
  				color #999999
  				font-size 12px
  			.value
  				display block
  				margin-top 10px
  				text-align center
  				color #333333
  				font-size 30px
  				font-weight bold
  				.unit
  					font-size 14px
  		.right
  			flex 1
  			.name
  				display block
  				margin-top 15px
  				text-align center
  				color #999999
  				font-size 12px
  			.value
  				display block
  				margin-top 10px
  				text-align center
  				color #333333
  				font-size 30px
  				font-weight bold
  				.unit
  					font-size 14px
</style>
