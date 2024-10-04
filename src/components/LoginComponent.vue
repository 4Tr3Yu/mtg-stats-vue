<script setup lang="ts">
import { ref, reactive } from 'vue'
import { supabase } from '../supabaseClient'
import { useLoaderStore } from '@/stores/loaderStore';
import AlertMessage from './UI/AlertMessage.vue';
const loaderStore = useLoaderStore();


const loading = loaderStore.isLoading
const email = ref('')
const alertMessage = reactive({
	message: 'this is a test msg',
	alertType: 'Info',
	showAlert: false,
})

const handleLogin = async () => {
	try {
		loaderStore.setLoading(true)
		const { error } = await supabase.auth.signInWithOtp({
			email: email.value,
		})
		if (error) throw error
		alertMessage.message = 'Check your email for the login link'
		alertMessage.alertType = 'Success'
		alertMessage.showAlert = true
	} catch (error) {
		if (error instanceof Error) {
			alertMessage.message = error.message
			alertMessage.alertType = 'Error'
			alertMessage.showAlert = true
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
		<AlertMessage v-if="alertMessage.showAlert" :message="alertMessage.message" :alert-type="alertMessage.alertType"
			@close="alertMessage.showAlert = false" />
	</form>
</template>