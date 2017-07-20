<template>
	<div id="app">
		<router-view></router-view>
	</div>
</template>

<script>
export default {
	name: 'app'
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Cabin');

body {
	background: linear-gradient(to bottom right, #444, #222);
	min-height: 100vh;
}

$font-family: 'Cabin', 'Avenir', Helvetica, Arial, sans-serif;

$font-dark: #444;

#app {
	font-family: $font-family;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;

	display: flex;
	align-items: center;
	justify-content: center;

	min-height: 100vh;

	color: $font-dark;
}

input {
	font-family: $font-family;
}
</style>
