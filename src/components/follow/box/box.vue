<template>
	<section class='box'>
		<div class='title .clearfix'>
			<slot name="name">
				<h3 v-text="title"></h3>
			</slot>
			<slot name="more">
				<a class='more' :href="href">
					{{more}}
					<i v-if="!!more" class='fa fa-angle-right'></i>
				</a>
			</slot>
		</div>
		<div class='content'>
			<slot></slot>
		</div>
	</section>
</template>

<script>
	export default {
		props: {
			title: String,
			more: String,
			href: String
		}
	}
</script>

<style lang='stylus' scoped>
@import '../../../common/stylus/config'
.box
	margin-bottom: 10px
	background: #fff
	> .title
		padding: 0px 10px
		height: 50px
		line-height: 50px
		border-bottom: 1px solid #ccc
		h3
			float: left
			font-size: 1rem
		.more
			float: right
			font-size: 0.8rem
			color: import-font-color
			span
				color: #999999
	.content
		padding-top: 20px
		padding-bottom: 20px
</style>
