<template>
	<header class="shadow bg-white">
		<div class="container p-3 p-md-4 d-flex justify-content-between align-items-center">
			<div>
				<a href="/">
					<i class="fas fa-home fa-3x"></i>
				</a>
			</div>

			<div class="h1 mb-0">
				<a class="mr-4" :href="link.contact">
					<i class="fas fa-envelope"></i>
				</a>
				<a class="mr-4" :href="link.twitter">
					<i class="fab fa-twitter"></i>
				</a>
				<a class="mr-0" :href="link.github">
					<i class="fab fa-github"></i>
				</a>
			</div>
		</div>
	</header>
</template>


<script>
export default {
	data: function() {
		return {
			link: {
				twitter: process.env.link.twitter,
				contact: process.env.link.contact,
				telegram: process.env.link.telegram,
				github: process.env.link.github
			}
		};
	}
};
</script>