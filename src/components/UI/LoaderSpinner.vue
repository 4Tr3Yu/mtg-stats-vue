<template>
	<div class="flex items-center flex-col justify-center h-screen absolute top-0 left-0 w-full bg-black/80 z-20">
		<div class="spinner-border animate-spin inline-block w-12 h-12 border-4 rounded-full mb-4" role="status">
		</div>
		<span class="visually-hidden">Loading...</span>
	</div>
</template>
<style scoped>
.spinner-border {
	@apply border-sky-500 bg-gradient-to-r from-sky-950 to-transparent;
	/* Customize your spinner color here */
	border-bottom: transparent;
	border-top: transparent;
}
</style>