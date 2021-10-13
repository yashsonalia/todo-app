<template>
	<div id="app" class="app">
		<router-view />
		<nav class="nav" id="nav">
			<div class="nav-list">
				<router-link to="/">Home</router-link> |
				<router-link to="/about">About</router-link>
			</div>
		</nav>
	</div>
</template>

<style lang="scss" scoped>
a.router-link-exact-active {
	color: hsl(130, 91%, 50%);
}
</style>

