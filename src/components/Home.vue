<template>
	<div>
    	<Header />
		<h1>Welcome to home page, {{ name }}</h1>
		<div class="list">
			<table border="1">
				<tr>
					<td>Id</td>
					<td>Name</td>
					<td>Contract</td>
					<td>Address</td>
					<td>Action</td>
				</tr>
				<tr v-for="item in resturant" :key="item.id">
					<td>{{item.id}}</td>
					<td>{{item.name}}</td>
					<td>{{item.contract}}</td>
					<td>{{item.address}}</td>
					<td>
						<button><router-link :to="'/update/'+item.id">Update</router-link></button>
						<button v-on:click="deleteResturant(item.id)">Delete</button>
					</td>
				</tr>
			</table>
		</div>
	</div>
</template>


<script>
import Header from './Header.vue';
import axios from 'axios';

export default {
	name:'Home',

	data(){
		return{
			name : '',
			resturant:[]
		}
	},
	
	components:{
		Header
	},

	methods:{
		async deleteResturant(id){
			let result = await axios.delete("http://localhost:3000/resturants/"+id);
			// console.warn(result.status);
			if(result.status == 200){
				alert('Resturant deleted successfully.');
				this.loadData();
			}else{
				alert('Error found!')
			}
		},
		async loadData(){
			let result = await axios.get("http://localhost:3000/resturants");
			this.resturant = result.data;
		}
	},

    async mounted() {
		let user = localStorage.getItem('user-info');
		
		if(!user){
			this.$router.push({name:'SignUp'})
		}
		this.name = JSON.parse(user).name;

		this.loadData();
	}
	
}
</script>


<style scoped>
	td{
		width: 160px;
		height: 40px;
	}
	td button{
		padding: 2px 5px;
		margin: 5px;
		background-color: yellow;
		font-size: 17px;
		/* display: flex; */
		text-align: center;
		cursor: pointer;
	}
	td button a{
		text-decoration: none;
		font-size: 17px;
		/* display: flex; */
		text-align: center;
	}
	.list{
		margin-left: 30px;
		margin-right: 30px;
	}
	table{
		width: 100%;
		/* border-collapse: collapse; */
	}
</style>