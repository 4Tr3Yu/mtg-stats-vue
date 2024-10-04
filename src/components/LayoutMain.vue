<script setup lang="ts">
import { ref } from 'vue';
import LoaderSpinner from './UI/LoaderSpinner.vue';
import { useLoaderStore } from '@/stores/loaderStore';
const loaderStore = useLoaderStore();

</script>
<template>
	<LoaderSpinner v-if="loaderStore.isLoading" />
	<header class="fixed bg-black/80 w-full h-12">
		<nav class="flex justify-center items-center gap-4 container h-full">
			<RouterLink to="/">Home</RouterLink>
			<RouterLink to="/about">About</RouterLink>
		</nav>
	</header>
	<main class="container mx-auto pt-12 flex justify-center items-center h-dvh">
		<slot />
	</main>
</template>