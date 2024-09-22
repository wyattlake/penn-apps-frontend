<script lang="ts">
	// login/+page.svelte
	import { session } from '$lib/session';
	import { auth, db } from '$lib/firebase.client';
	import * as firestore from 'firebase/firestore';
	import {
		GoogleAuthProvider,
		signInWithPopup,
		signInWithEmailAndPassword,
		type UserCredential
	} from 'firebase/auth';
	import { goto } from '$app/navigation';

	let email: string = '';
	let password: string = '';

	async function loginWithMail() {
		await signInWithEmailAndPassword(auth, email, password)
			.then((result) => {
				const { user }: UserCredential = result;
				// load from firestore "users" collection

				if (user!.uid != null) {
					localStorage.setItem('uid', user?.uid);
					goto('/dashboard');
				}
			})
			.catch((error) => {
				return error;
			});
	}
</script>

<div class="login-form">
	<h1>Login</h1>
	<form on:submit={loginWithMail}>
		<input bind:value={email} type="text" placeholder="Email" />
		<input bind:value={password} type="password" placeholder="Password" />
		<button type="submit">Login</button>
	</form>

	<div>or</div>
</div>
