<template>
    <div class="login-body">
		<img class="logo" alt="Vue logo" src="../assets/logo.svg">
		<h1>Login</h1>

		<div class="login">

			<input type="email" v-model="email" placeholder="Enter your email...">

			<input type="password" v-model="password" placeholder="Enter your password...">

			<button v-on:click="login">Login</button>
			<br>
			<button><router-link to="/sign-up">Sign Up</router-link></button>

		</div>
	</div>
</template>


<script>
// import { defineComponent } from '@vue/composition-api'
import axios from 'axios';
export default {
    name: 'Login',

	data(){
		return {
			email : '',
			password : ''
		}
	},

	methods:{
		async login(){
			let result = await axios.get(
				`http://localhost:3000/users?email=${this.email}&password=${this.password}`
			)
			console.warn(result);
			if(result.status == 200 && result.data.length > 0){
				alert('Login successful.');
				localStorage.setItem("user-info", JSON.stringify(result.data[0]))
				this.$router.push({name:'Home'})
			}else{
				alert('Error found!')
				this.$router.push({name:'Login'})
				
			}
			console.warn(result);
		}
	},

	mounted() {
		let user = localStorage.getItem('user-info')
		if(user){
			this.$router.push({name:'Home'})
		}
	}
}
</script>


<style scoped>
	.login-body{
		margin-top: 50px;
	}
	.login a{
		text-decoration: none;
		color: white;
	}
</style>
