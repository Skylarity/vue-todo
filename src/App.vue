<template>
	<div id="app">
		<h1>DO</h1>
		<router-view></router-view>
	</div>
</template>

<script>
export default {
	name: 'app'
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Cabin|Cabin+Sketch');

body {
	background: linear-gradient(to bottom right, #74ebd5, #ACB6E5);
	min-height: 100vh;
}

$title-font: 'Cabin Sketch', 'Avenir', Helvetica, Arial, sans-serif;
$font-family: 'Cabin', 'Avenir', Helvetica, Arial, sans-serif;

$font-dark: #444;

#app {
	font-family: $font-family;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;

	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;

	min-height: 100vh;

	color: $font-dark;

	h1 {
		margin: 0;

		font-family: $title-font;
		font-size: 8rem;
		color: rgba(#fff, .6);
	}
}

input {
	font-family: $font-family;
}
</style>
