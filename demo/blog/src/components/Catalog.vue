<!-- vue 模板文件-->
<template>
	<div class="catalogCom">
		<ul class="catalog-list">
			<li class="item-h2" v-for="(item, index) in catalog" :key="index">
				<a class="a-h2" :href="'#' + item.id" :title="item.innerHTML" :class="{'active':item.id === getCurCatalog}" @click="to(item.id)">{{item.innerHTML}}</a>
				<template v-if="item.children.length">
					<ul class="list-h3">
						<li class="item-h3" v-for="(item1, index1) in item.children" :key="index1">
							<a class="a-h3" :href="'#' + item1.id" :title="item1.innerHTML" :class="{'active':item1.id === getCurCatalog}" @click="to(item1.id)">{{item1.innerHTML}}</a>
							<template v-if="item1.children.length">
								<ul class="list-h4">
									<li class="item-h4" v-for="(item2, index2) in item1.children" :key="index2">
										<a class="a-h4" :href="'#' + item2.id" :title="item2.innerHTML" :class="{'active':item2.id === getCurCatalog}" @click="to(item2.id)">{{item2.innerHTML}}</a>
									</li>
								</ul>
							</template>
						</li>
					</ul>
				</template>
			</li>
		</ul>
	</div>
</template>

<script>

	export default {
		name: 'catalogCom',
		components: {
		},
		props:{
			catalog:Array
		},
		data() {
			return {
				
			}
		},
		computed: {
			getCurCatalog(){
				return this.$store.getters.getCurCatalog;
			}
		},
		created() {

		},
		mounted() {

		},
		methods: {
			//点击目录树跳转
			to(catalogName){
				this.$store.commit('updateCurCatalog', catalogName);
			}
		}

	}
</script>

<style lang="scss" scoped>
	.catalogCom{
		width: 100%;
		// 清除ul,li默认样式
		ul,li{ 
			padding:0;
			margin:0;
			list-style:none
		}
		.catalog-list{
			a{
				position: relative;
				display: block;
				white-space: nowrap;
				overflow: hidden;
				text-overflow: ellipsis;
				margin: 6px 0;
    		padding: 4px 0 4px 18px;
				&:hover{
					text-decoration: none;
				}	
				&::before{
					position: absolute;
					top: 50%;
					left: 5px;
					content: "";
					margin-top: -3px;
					background-color: currentColor;
					border-radius: 50%;
				}
				&.a-h2::before{
					width: 6px;
					height: 6px;
				}
				&.a-h3::before,
				&.a-h4::before{
					width: 4px;
					height: 4px;
				}
				&.active{
					color: #007fff;
				}
			}
			.list-h3,
			.list-h4{
				margin-left: 20px;
			}
		}
	}

</style>