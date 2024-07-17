<template>
	<div class="register-body">
		<img class="logo" alt="Vue logo" src="../assets/logo.svg">
		<h1>Sign Up</h1>

		<div class="register">
			<input type="text" v-model="name" placeholder="Enter your name...">

			<input type="email" v-model="email" placeholder="Enter your email...">

			<input type="password" v-model="password" placeholder="Enter your password...">

			<button v-on:click="signUp">Sign Up</button>
			<br>
			<button><router-link to="/login">Login</router-link></button>
		</div>
	</div>
</template>



<script>
// import { defineComponent } from '@vue/composition-api'
import axios from 'axios'

export default {
    name : 'SignUp',
	data(){
		return{
			name:'',
			email:'',
			password:''
		}
	},

	methods:{
		async signUp(){
			let result = await axios.post("http://localhost:3000/users",{
				name:this.name,
				email:this.email,
				password:this.password
			});
			console.log(result);

			if(result.status == 201){
				alert('Sign up successful.');
				localStorage.setItem("user-info", JSON.stringify(result.data))
				this.$router.push({name:'Home'})
			}else{
				alert('Error found!')
				
			}
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
	.register-body{
		margin-top: 50px;
	}
	.register a{
		text-decoration: none;
		color: white;
	}
</style>
