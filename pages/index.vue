<template>
	<section class="container px-2 py-4 py-md-5">
		<div
			:key="article.slug"
			class="bg-white position-relative border border-primary rounded shadow px-3 px-md-5 py-4 py-md-5 my-3"
			v-for="article in articles"
		>
			<div class="text-muted text-small">
				<i class="far fa-clock mr-2"></i>
				<span>{{ new Date(article.createdAt).toLocaleDateString('en-NG', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}}</span>
			</div>

			<a :href="'/' + article.slug" class="stretched-link">
				<h1 class="mt-0 mb-2">{{article.title}}</h1>
			</a>

			<div class="text-muted lead">{{ article.description }}</div>
		</div>
	</section>
</template>


<script>
export default {
	layout: "blog",
	data: function() {
		return {};
	},

	head() {
		return {
			title: "OgbeniHMMD's Blog"
		};
	},

	async asyncData({ $content, params, error }) {
		let articles;

		try {
			articles = await $content("articles")
				.only(["title", "slug", "tags", "createdAt", "description"])
				.fetch();
		} catch (e) {
			return error({ statusCode: 404, message: "Page not found" });
		}

		return {
			articles
		};
	}
};
</script>