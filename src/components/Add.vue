<template>
	<div>
    	<Header />
		<h1>Welcome to Add Restaurant page</h1>
		<div class="add">
			<input type="text" v-model="resturant.name" placeholder="Enter your name...">

			<input type="text" v-model="resturant.contract" placeholder="Enter your contract...">

			<input type="text" v-model="resturant.address" placeholder="Enter your address...">

			<button v-on:click="addRestutant">Add Restaurant</button>

		</div>
	</div>
</template>


<script>
import Header from './Header.vue';
import axios from 'axios';

export default {
	name:'Add',
	components:{
		Header
	},

	data(){
		return{
			resturant:{
				name : '',
				contract : '',
				address : ''
			}
		}
	}, 

	methods:{
		
		async addRestutant(){
			console.warn(this.resturant);
			let result = await axios.post("http://localhost:3000/resturants", {
				name:this.resturant.name,
				contract:this.resturant.contract,
				address:this.resturant.address
			});
			// console.warn(result);

			if(result.status == 201){
				alert('Resturant added successfully.');
				// localStorage.setItem("user-info", JSON.stringify(result.data))
				this.$router.push({name:'Home'})
			}else{
				alert('Error found!')
				
			}
		}
	},

    mounted() {
		let user = localStorage.getItem('user-info')
		if(!user){
			this.$router.push({name:'SignUp'})
		}
	}
	
}
</script>


<style>
	.add input{
		width: 400px;
		height: 30px;
		padding-left: 20px;
		display: block;
		margin-bottom: 15px;
		margin-left: auto;
		margin-right: auto;
		border: 1px solid skyblue;
	}
	.add button{
		width: 400px;
		height: 40px;
		border: 1px solid skyblue;
		background-color: skyblue;
		font-size: 17px;
		font-weight: lighter;
		color: white;
		cursor: pointer;
	}
	.add button:hover{
		
		background-color: blue;
		
	}
</style>