<script setup lang="ts">
import { onMounted, ref } from 'vue';
import LoginView from '../components/LoginComponent.vue';
import ProfileView from '../components/ProfileComponent.vue';
import { supabase } from '../supabaseClient';

const session = ref()

onMounted(() => {
  supabase.auth.getSession().then(({ data }) => {
    console.log(data)
    session.value = data.session
  })

  supabase.auth.onAuthStateChange((_, _session) => {
    console.log(_session)
    session.value = _session
  })
})
</script>
<template>
  <ProfileView v-if="session" :session="session" />
  <LoginView v-else />
</template>
