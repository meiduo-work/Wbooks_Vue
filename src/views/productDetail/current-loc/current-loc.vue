<template>
	<div class="current-loc">
		<div class="breadcrumbs cle z-detail-box">
			<div class="menus">
				<a href="/">首页</a>
				<code>&gt;</code>
				<router-link :to="'/app/home/list/'+category.id">{{category.name}}</router-link>
				<code>&gt;</code>
				{{this.goods_name}}
			</div>
		</div>
	</div>
</template>
<script>
import { getGoodsDetail } from '../../../api/api';
export default {
	data() {
		return {
			proDetail: '',
			category: '',
			goods_name:'',
		};
	},
	components: {},
	props: {},
	created() {
		this.getloc();
	},
	watch: {},
	computed: {},
	methods: {
		getloc() {
			var id = this.$route.params.productId;
			//  请求商品详情
			getGoodsDetail(id)
				.then(response => {
					this.category = response.data['category'];
					this.goods_name = response.data["name"];
				})
				.catch(function(error) {
					console.log(error);
				});
		}
	}
};
</script>
<style lang="scss">
.cle:after {
	visibility: hidden;
	display: block;
	font-size: 0;
	content: '\20';
	clear: both;
	height: 0;
}
.cle {
	*zoom: 1;
}

a {
	text-decoration: none;
	color: #333;
	-webkit-transition: color 0.2s;
	-moz-transition: color 0.2s;
	-o-transition: color 0.2s;
	-ms-transition: color 0.2s;
	transition: color 0.2s;
}
a:hover {
	color: #ff3030;
}
a:focus,
area:focus {
	outline: 0;
}

canvas {
	-ms-touch-action: double-tap-zoom;
}

.breadcrumbs {
	padding: 0 5px 0 0;
	line-height: 38px;
	color: #666;
}
.breadcrumbs .menus {
	float: left;
}
.breadcrumbs .menus a {
	margin-right: 6px;
}
.breadcrumbs .right {
	float: right;
	color: #bbb;
}
.breadcrumbs .right i {
	font-size: 20px;
	margin-right: 5px;
	vertical-align: -2px;
}
.breadcrumbs .right .code {
	color: #fafafa;
	margin-right: 30px;
	display: inline-block;
}
</style>
