<script lang="ts">
	import Navbar from '../Components/Navbar.svelte';
	import Footer from '../Components/Footer.svelte';
	import Intro from '../Components/Intro.svelte';
	import Meta from '../Meta/Meta.svelte';
	import '@fortawesome/fontawesome-free/css/all.css';
	import '@picocss/pico';
	import '../app.css';
</script>

<Meta />

<div class="w-full h-full fixed top-0 z-0" />
<Navbar />
<Intro />
<main class="relative">
	<slot />
</main>
<Footer />
