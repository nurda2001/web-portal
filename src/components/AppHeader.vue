<template>
	<div>
		<v-navigation-drawer  absolute temporary v-model="drawer" class="hidden-md-and-up">
		<v-list>
			<v-list-tile v-for="(item,i) in menuItems" :key="`navdrawer${i}`" :to="item.route">
				<v-list-tile-action>
					<v-icon v-html="item.icon"></v-icon>
				</v-list-tile-action>
				<v-list-tile-content>
						<v-list-tile-title v-text="item.title"></v-list-tile-title>
					</v-list-tile-content>
			</v-list-tile>
		</v-list>
		</v-navigation-drawer>
		<v-toolbar  fixed app color="White">
			<v-toolbar-side-icon class="hidden-md-and-up" @click.stop="drawer = !drawer"></v-toolbar-side-icon>
			<router-link to="/" tag="span" style=" cursor: pointer">
			<v-toolbar-title v-text="'CyberSport News'" class="black--text"></v-toolbar-title>
		</router-link>
		<v-toolbar-title v-text="''" style="font-weight: 300; font-size: 15px" class="hidden-sm-and-down"></v-toolbar-title>
			<v-spacer></v-spacer>
			<v-toolbar-items class="hidden-sm-and-down">
				<v-btn v-for="(item, i) in menuItems" flat :key="`menuItem${i}`" :to="item.route" >
					{{item.title}}
				</v-btn>

			</v-toolbar-items>
		</v-toolbar>
	</div>	
</template>

<script>
	export default{
		data(){
			return{
				drawer: false
			}
		},
		computed:{
			isUserAutheticated(){
        return this.$store.getters.isUserAutheticated
      },
			menuItems(){
				return this.isUserAutheticated ?
				[
				       {
                       	title: 'News',
                       	route: '/news'
                       },
                       {
                       	title: 'Создание',
                       	route: '/creatingNews'
                       },
                         
				] : [
                   
                       {
                       	title: 'Новости',
                       	route: '/news'
                       },
                       {
                        title: 'Sign in',
                        route : '/signin'
                       },
                       {
                       title: 'Sign Up',
                       route: '/'
                       }
				]
			}
		},
		watch:{
      isUserAutheticated(val){
        if(val === false)
          this.$router.push({ name: 'home' })
      }
    }
	}
</script>

<style scoped>
	v-btn{
		text-decoration-style: none!important;
	}
</style>