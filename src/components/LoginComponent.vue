<script setup lang="ts">
import { ref } from 'vue'
import { supabase } from '../supabaseClient'
import { useLoaderStore } from '@/stores/loaderStore';
const loaderStore = useLoaderStore();


const loading = loaderStore.isLoading
const email = ref('')

const handleLogin = async () => {
	try {
		loaderStore.setLoading(true)
		const { error } = await supabase.auth.signInWithOtp({
			email: email.value,
		})
		if (error) throw error
		alert('Check your email for the login link!')
	} catch (error) {
		if (error instanceof Error) {
			alert(error.message)
		}
	} finally {
		loaderStore.setLoading(false)
	}
}

</script>

<template>

	<form
		class="min-w-80 flex flex-col gap-4 justify-center p-4 border border-sky-900 rounded-lg bg-gradient-to-tl from-sky-950 to-transparent"
		@submit.prevent="handleLogin">
		<p class="font-bold">Sing in just with you email</p>
		<input class="w-full bg-transparent border-sky-950 border pl-4 p-2 rounded-full" name="email"
			autocomplete="email" required type="email" placeholder="Your email" v-model="email" />
		<input type="submit"
			class=" cursor-pointer flex-grow-0 bg-sky-300/10 rounded-full p-2 hover:bg-sky-300/30 hover:font-bold hover:scale-105 duration-300 ease-out"
			:value="loading ? 'Loading' : 'Sing In'" :disabled="loading" />
	</form>
</template>