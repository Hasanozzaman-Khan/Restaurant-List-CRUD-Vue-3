<template>
	<div>
    	<Header />
		<h1>Welcome to Update Restaurant page</h1>
		<from class="update">
			<input type="text" v-model="resturant.name" value="resturant.name" placeholder="Enter your name...">

			<input type="text" v-model="resturant.contract" placeholder="Enter your contract...">

			<input type="text" v-model="resturant.address" placeholder="Enter your address...">

			<button v-on:click="updateRestutant">Add Restaurant</button>

		</from>
	</div>
</template>


<script>
import Header from './Header.vue';
import axios from 'axios';

export default {
	name:'Update',
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
		async updateRestutant(){
			console.warn(this.resturant);
			let result = await axios.put("http://localhost:3000/resturants/"+this.$route.params.id, {
				name:this.resturant.name,
				contract:this.resturant.contract,
				address:this.resturant.address
			});
			// console.warn(result);

			if(result.status == 200){
				alert('Resturant updated successfully.');
				// localStorage.setItem("user-info", JSON.stringify(result.data))
				this.$router.push({name:'Home'})
			}else{
				alert('Error found!')
				
			}
		}
	},

    async mounted() {
		let user = localStorage.getItem('user-info')
		if(!user){
			this.$router.push({name:'SignUp'})
		}
		
		let result = await axios.get('http://localhost:3000/resturants/'+this.$route.params.id);
		this.resturant = result.data;
		console.warn(result.data);
	}
	
}
</script>


<style>

</style>