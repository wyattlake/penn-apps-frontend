<script>
	// import { authClient, fetchAuthenticationInfo } from '$lib/auth';
	import { goto } from '$app/navigation';
    import { onMount } from 'svelte';
    import { session } from '$lib/session';
    import { auth, db } from '$lib/firebase.client';

    onMount(async () => {
        if (auth.currentUser) {
            goto('/dashboard');
        }
    });
</script>

<h1>Welcome to Our App!</h1>

<a href="/signup">Sign up</a>
<a href="/login">Log in</a>