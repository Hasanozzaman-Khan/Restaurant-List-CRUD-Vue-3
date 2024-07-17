<template>

    <router-view />

</template>

<script>



export default {
  name: 'App',
  
}
</script>

<style>
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		/* color: #2c3e50; */
		/* margin-top: 20px; */
	}
	body{
		padding: 0;
		margin: 0;
	}
	.logo{
		width: 100px;
	}
	.register input, .login input, .update input{
		width: 400px;
		height: 30px;
		padding-left: 20px;
		display: block;
		margin-bottom: 15px;
		margin-left: auto;
		margin-right: auto;
		border: 1px solid skyblue;
	}
	.register button, .login button, .update button{
		width: 400px;
		height: 40px;
		border: 1px solid skyblue;
		background-color: skyblue;
		font-size: large;
		font-weight: bold;
		color: white;
		cursor: pointer;
		margin-bottom: 10px;
	}
</style>
