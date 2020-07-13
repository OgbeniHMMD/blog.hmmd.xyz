<template>
	<section class="container px-2 py-4 py-md-5">
		<header class="text-center border-bottom pb-4">
			<h1 class="mb-4 display-4">{{article.title}}</h1>
			<div class="text-muted">
				<i class="far fa-clock mr-2"></i>
				<span>{{ new Date(article.createdAt).toLocaleDateString('en-NG', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}}</span>
			</div>
		</header>

		<nuxt-content :document="article" class="mt-4 lead" />

		<div class="mt-4">
			<vue-disqus
				shortname="hmmd"
				:identifier="$route.params.slug"
				:url="`https://blog.hmmd.xyz/${$nuxt.$route.fullPath}`"
			></vue-disqus>
		</div>
	</section>
</template>


<script>
export default {
	head() {
		return {
			title: this.article.title + " - " + process.env.blog.name,
			meta: [
				{
					hid: "description",
					name: "description",
					content: this.article.description
				},
				// Open Graph
				{ hid: "og:title", property: "og:title", content: this.article.title },
				{
					hid: "og:description",
					property: "og:description",
					content: this.article.description
				},
				// Twitter Card
				{
					hid: "twitter:title",
					name: "twitter:title",
					content: this.article.title
				},
				{
					hid: "twitter:description",
					name: "twitter:description",
					content: this.article.description
				}
			]
		};
	},

	async asyncData({ $content, params, error }) {
		// load content from the '/content/artices' directory

		let article;
		const slug = "articles/" + params.slug;

		try {
			article = await $content(slug).fetch();
		} catch (e) {
			return error({ statusCode: 404, message: "Page not found" });
		}

		return {
			article
		};
	}
};
</script>
