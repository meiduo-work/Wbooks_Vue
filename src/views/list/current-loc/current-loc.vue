<template>
    <div class="current-loc">
        <div class="breadcrumbs cle">
          <div class="menus">
           <a href="/">首页</a>
           <code>&gt;</code>
           <router-link :to="'/app/home/list/'+top_category.id">{{top_category.name}}</router-link>
          </div>
      </div>
    
    </div>
  
</template>
<script>
  import { getGoods,getCategory } from '../../../api/api';
  export default {
    data () {
        return {
            top_category:'',
        };
    },
    components: {
        
    },
    created () {
        this.getloc();
    },
    watch: {
        
    },
    computed: {

    },
    methods: {
        getloc(){
			console.log(111);
			var top_category = this.$route.params.id;
			console.log(top_category);
			getGoods({
				top_category:top_category
			}).then(response => {
					// console.log(222);
					var category = response.data["results"][0]["category"]["parent_category"];
					getCategory({
						id:category
					}).then(response=>{
						this.top_category = response.data
						console.log(this.top_category);
					}).catch(function(error) {
					console.log(error);
				});
				}).catch(function(error) {
					console.log(error);
				});
		}
    }
}
</script>
<style  lang='scss'>
.cle:after{
    visibility:hidden;
    display:block;
    font-size:0;
    content:'\20';
    clear:both;
    height:0
}
.cle{
    *zoom:1
}

a {
    text-decoration:none;
    color:#333;
    -webkit-transition:color .2s;
    -moz-transition:color .2s;
    -o-transition:color .2s;
    -ms-transition:color .2s;
    transition:color .2s
}
a:hover {
    color:#09c762
}
a:focus,area:focus {
    outline:0
}

canvas {
    -ms-touch-action:double-tap-zoom
}

.breadcrumbs {
    padding:0 5px 0 0;
    line-height:38px;
    color:#666
}
.breadcrumbs .menus {
    float:left
}
.breadcrumbs .menus a {
    /*margin-right:6px*/
    margin-left: 6px;
    margin-right: 6px;
}
.breadcrumbs .right {
    float:right;
    color:#bbb
}
.breadcrumbs .right i {
    font-size:20px;
    margin-right:5px;
    vertical-align:-2px
}
.breadcrumbs .right .code {
    color:#fafafa;
    margin-right:30px;
    display:inline-block
}

</style>
