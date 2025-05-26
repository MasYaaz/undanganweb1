<!-- App.svelte -->
<script lang="ts">
	import { onMount } from 'svelte';
	import { browser } from '$app/environment'; // Gunakan ini untuk cek localStorage aman
	import { FontAwesomeIcon } from '@fortawesome/svelte-fontawesome';
	import { faChevronDown } from '@fortawesome/free-solid-svg-icons';
	import Countdown from '$lib/components/Countdown.svelte';
	import Navbar from '$lib/components/Navbar.svelte'; //Import Navbar Component
	import { slide } from 'svelte/transition';

	let targetSection: HTMLDivElement;
	let showIntro = true; // Variabel untuk menunjukkan halaman utama

	const targetDate = new Date('2025-06-15T10:00:00'); // Variabel buat tanggal countdown

	// Fungsi agar tidak bisa masuk ke section1 (halaman utama) dan aktifkan fungsi scroll
	function enterInvitation() {
		showIntro = false; // Menyembunyikan Intro undangan
		localStorage.setItem('hasEntered', 'true'); // buat menyimpan di local storage jadi tidak bisa membuka kop undangan
		document.body.style.overflow = 'auto'; // Aktifkan scroll
		targetSection.scrollIntoView({ behavior: 'smooth' });
	}
</script>

{#if showIntro}
	<!-- SECTION 1: Hero dengan Countdown dan Tombol Scroll -->
	<section
		in:slide={{ duration: 1000 }}
		out:slide={{ duration: 2000 }}
		class="flex h-screen flex-col items-center justify-center bg-pink-100 px-4 text-center"
	>
		<h2 class="mb-4 text-3xl font-bold md:text-5xl">Kami Akan Menikah</h2>

		<Countdown {targetDate} />

		<button
			class="mt-6 flex items-center gap-2 rounded-full bg-pink-500 px-6 py-3 text-white hover:cursor-pointer hover:bg-pink-600"
			on:click={enterInvitation}
		>
			Lihat Undangan
			<FontAwesomeIcon icon={faChevronDown} class="animate-bounce" />
		</button>
	</section>
{:else}
	<!-- NAVBAR -->
	<Navbar show={!showIntro} />

	<!-- SECTION CONTAINER SCROLLABLE -->
	<div bind:this={targetSection} class:scrollable={!showIntro} class="transition-all duration-700">
		<!-- SECTION 2 -->
		<section id="section2" class="flex h-screen items-center justify-center bg-white px-4">
			<div class="text-center">
				<h2 class="mb-2 text-2xl font-semibold">Cerita Cinta Kami</h2>
				<p class="mx-auto max-w-xl text-gray-600">
					Kami bertemu, jatuh cinta, dan memutuskan untuk bersama selamanya...
				</p>
			</div>
		</section>

		<!-- SECTION 3 -->
		<section id="section3" class="flex h-screen items-center justify-center bg-pink-50 px-4">
			<div class="text-center">
				<h2 class="mb-2 text-2xl font-semibold">Detail Acara</h2>
				<p class="text-gray-600">Sabtu, 15 Juni 2025 • Gedung Bahagia • 10:00 WIB</p>
			</div>
		</section>

		<!-- SECTION 4 -->
		<section id="section4" class="flex h-screen items-center justify-center bg-white px-4">
			<div class="text-center">
				<h2 class="mb-2 text-2xl font-semibold">Galeri Kenangan</h2>
				<p class="text-gray-600">Beberapa momen spesial kami bersama.</p>
			</div>
		</section>

		<!-- SECTION 5 -->
		<section id="section5" class="flex h-screen items-center justify-center bg-pink-100 px-4">
			<div class="text-center">
				<h2 class="mb-2 text-2xl font-semibold">Ucapan & Doa</h2>
				<p class="text-gray-600">Kami sangat menghargai ucapan dan doa dari Anda.</p>
			</div>
		</section>
	</div>
{/if}

<style>
</style>
