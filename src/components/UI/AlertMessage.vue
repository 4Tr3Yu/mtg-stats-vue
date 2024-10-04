<script setup lang="ts">
import { reactive } from 'vue';

const props = defineProps({
	message: String,
	alertType: {
		type: String,
		default: 'Error',
	},
});

defineEmits(['close']);

const { alertType } = props;

const classObject = reactive({
	'alert-box--error': alertType === 'Error',
	'alert-box--success': alertType === 'Success',
	'alert-box--warning': alertType === 'Warning',
	'alert-box--info': alertType === 'Info',
});
</script>
<template>
	<div class="w-full alert-box border bg-gradient-to-bl px-3 py-2 rounded-lg relative" :class="classObject">

		<h2 class="text-xs font-bold capitalize">{{ alertType }}</h2>
		<p class="font-thin">{{ message }}</p>
		<button @click="$emit('close')"
			class="absolute right-0 top-0 h-full w-6 flex items-center justify-center border-l bg-white/15 rounded-r-lg">
			<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
				stroke="currentColor">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
			</svg>
		</button>
	</div>
</template>
<style scoped lang="scss">
.alert-box {
	&--error {
		@apply border-rose-400 from-rose-400/75 to-transparent text-rose-200;
	}

	&--success {
		@apply border-emerald-400 from-emerald-400/75 to-transparent text-emerald-200;
	}

	&--warning {
		@apply border-amber-400 from-amber-400/75 to-transparent text-amber-200;
	}

	&--info {
		@apply border-sky-400 from-sky-400/75 to-transparent text-sky-200;

	}

}
</style>