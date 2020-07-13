<template>
	<div class="v-center min-vh-75 p-2">
		<div class="text-center">
			<div class="display-3">{{error.statusCode}} Error!</div>
			<div class="display-4">{{error.message}}</div>

			<div class="display-1">
				<i class="far fa-frown"></i>
			</div>
		</div>
	</div>
</template>


<script>
export default {
	props: {
		error: {
			type: Object,
			default: null
		}
	},
	head() {
		return {
			title: this.error.message + " - " + process.env.blog.name
		};
	}
};
</script>