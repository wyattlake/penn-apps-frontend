<script lang="ts">
	// register/+page.svelte
	import { auth, db } from '$lib/firebase.client';
	import * as firestore from 'firebase/firestore';
	import { createUserWithEmailAndPassword } from 'firebase/auth';
	import { goto } from '$app/navigation';
	import { session } from '$lib/session';

	let email: string = '';
	let password: string = '';
	let companyName: string = '';
	let yelp: string = '';
	let streetName: string = '';
	let city: string = '';
	let state: string = '';
	let zipCode: string = '';

	async function handleRegister() {
		await createUserWithEmailAndPassword(auth, email, password)
			.then((result) => {
				const docRef = firestore.doc(db, 'users', user?.uid);
				firestore
					.setDoc(docRef, {
						displayName: companyName,
						email: email,
						location: {
							streetName: streetName,
							city: city,
							state: state,
							zipCode: zipCode
						},
						yelp: yelp
					})
					.then(() => {
						if (user!.uid != null) {
							localStorage.setItem('uid', user?.uid);
							goto('/dashboard');
						}
						goto('/');
					});
			})
			.catch((error) => {
				throw new Error(error);
			});
	}
</script>

<!-- register/+page.svelte -->
<div class="register-form">
	<form on:submit={handleRegister}>
		<h2>Register</h2>
		<input bind:value={email} type="text" placeholder="Email" />
		<input bind:value={password} type="password" placeholder="Password" />
		<!-- make fields for company name, yelp, all required -->
		<input bind:value={companyName} type="text" placeholder="Company Name" required />
		<input bind:value={yelp} type="text" placeholder="Yelp" required />
		<!-- make required fields of street name, city, state, zip code -->
		<input bind:value={streetName} type="text" placeholder="Street Name" required />
		<input bind:value={city} type="text" placeholder="City" required />
		<input bind:value={state} type="text" placeholder="State" required />
		<input bind:value={zipCode} type="text" placeholder="Zip Code" required />
		<button type="submit">Register</button>
	</form>
</div>
