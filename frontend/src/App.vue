<template>
	<div id="app" :class="{'hide-menu': !isMenuVisible || !user}">
		<Header title="Cod3r - Base de Conhecimento" 
		:hideToggle="!user"
		:hideUserDropDown="!user"/>
		<Menu v-if="user"/>
		<Loading v-if="validatingToken"/>
		<Content v-else/>
		<Footer />
	</div>
</template>

<script>
import axios from "axios"
import{baseApiUrl, userKey} from "@/global"
import {mapState} from "vuex"
import Header from "@/components/templates/Header"
import Menu from "@/components/templates/Menu"
import Content from "@/components/templates/Content"
import Footer from "@/components/templates/Footer"
import Loading from "@/components/templates/Loading"
export default {
	name: "App",
	components: {Header, Menu, Content, Footer, Loading},
	computed: mapState(['isMenuVisible', 'user']),
	data: function(){
		return{			
			validatingToken: true
		}
	},
	methods: {
		async validateToken(){

			this.validatingToken = true

			const json = localStorage.getItem(userKey)
			const userData = JSON.parse(json)
			this.$store.commit('setUser', null)

			if(!userData){
				this.validatingToken = false
				this.$router.push({name: 'auth'})
				return
			}

			const res = await axios.post(`${baseApiUrl}/validateToken`, userData)

			if(!res.data){
				this.$store.commit('setUser', userData)
			} else {
				localStorage.removeItem(userKey)
				this.$router.push({name: 'auth'})				
			}
			this.validatingToken = false
		}
	},
	created(){
		this.validateToken()
	}
}
</script>

<style>
	*{
		font-family: "Lato", sans-serif;
	}
	body{
		margin: 0;
	}
	#app{
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smooth: greyscale;

		height: 100vh;
		display: grid;
		grid-template-rows: 60px 1fr 40px;
		grid-template-columns: 240px 1fr;
		grid-template-areas: 
			"header header"
			"menu content"
			"footer footer";
	}
	#app.hide-menu{
		grid-template-areas: 
			"header header"
			"content content"
			"footer footer";
	}
</style>