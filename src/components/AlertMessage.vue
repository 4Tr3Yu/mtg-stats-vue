<script setup lang="ts">
defineProps(['message'])
</script>
<template>
	<div class="border border-rose-400 p-4 rounded-lg ">
		<h2>Error</h2>
		<p>{{ message }}</p>
	</div>
</template>