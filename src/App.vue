<template>
	<div id="app" class="app">
		<main>
			<router-view />
		</main>
		<footer class="footer" id="footer">
			<div class="footer-nav">
				<router-link to="/">Home</router-link> |
				<router-link to="/about">About</router-link>
			</div>
		</footer>
	</div>
</template>

<style lang="scss" scoped>
a.router-link-exact-active {
	color: hsl(130, 91%, 50%);
}
</style>

