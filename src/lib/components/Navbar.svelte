<!-- src/lib/components/Navbar.svelte -->
<script lang="ts">
	import { onMount } from 'svelte';
	import { FontAwesomeIcon } from '@fortawesome/svelte-fontawesome';
	import {
		faPerson,
		faPersonDress,
		faCalendarCheck,
		faImage,
		faRectangleList,
		faEnvelopeOpen,
		faHomeUser

	} from '@fortawesome/free-solid-svg-icons';

	export let show = true; // dikontrol dari luar
	let activeSection = 'section2'; // default

	// Fungsi scroll ke ID tertentu
	function scrollToSection(id: string) {
		const section = document.getElementById(id);
		if (section) {
			section.scrollIntoView({ behavior: 'smooth' });
		}
	}

	const navItems = [
		{
			id: 'section2',
			icon: [faHomeUser],
			label: 'Home'
		},
		{
			id: 'section3',
			icon: [faPerson, faPersonDress],
			label: 'Mempelai'
		},
		{
			id: 'section4',
			icon: [faCalendarCheck],
			label: 'Acara'
		},
		{
			id: 'section5',
			icon: [faImage],
			label: 'Galeri'
		},
		{
			id: 'section6',
			icon: [faRectangleList],
			label: 'RSVP'
		}
	];
	// Setup observer untuk mendeteksi section aktif
	onMount(() => {
		const observer = new IntersectionObserver(
			(entries) => {
				for (const entry of entries) {
					if (entry.isIntersecting) {
						activeSection = entry.target.id;
					}
				}
			},
			{ rootMargin: '0px 0px -40% 0px', threshold: 0.1 }
		);

		navItems.forEach((item) => {
			const section = document.getElementById(item.id);
			if (section) {
				observer.observe(section);
			}
		});
	});
</script>

{#if show}
	<!-- ini Navbar bagian atas -->
	<nav
		class="fixed top-0 z-50 flex w-full items-center justify-center bg-white/30 px-6 py-2 md:py-4 shadow backdrop-blur-md"
	>
		<h1 class="text-lg font-lora uppercase font-bold">
			<FontAwesomeIcon icon={faEnvelopeOpen} /> Undangan Digital
		</h1>
	</nav>

	<!-- Ini navbar bagian bawah -->
	<nav
		class="fixed bottom-0 z-50 flex w-full items-center justify-center bg-white/30 px-6 py-2 md:py-4 shadow backdrop-blur-md"
	>
		<ul class="flex gap-6 md:gap-20 text-center text-sm">
			{#each navItems as item}
				<li>
					<button
						on:click={() => scrollToSection(item.id)}
						class={`flex flex-col lg:flex-row items-center transition-transform duration-300 hover:scale-105 hover:cursor-pointer 
						${activeSection === item.id ? 'text-pink-600 font-bold scale-105' : ''}`}
					>
						<!-- Icon Section -->
						<div class="flex">
							{#each item.icon as ic, i}
								<FontAwesomeIcon
									icon={ic}
									class="fa-2x {i === 1 ? 'text-red-300' : 'font-medium'}"
								/>
							{/each}
						</div>

						<!-- Label -->
						<span
							class="uppercase mt-0.5 font-bold font-poppins text-[7px] md:mt-0 lg:text-2xl lg:ml-2 md:hover:font-black"
						>
							{item.label}
						</span>
					</button>
				</li>
			{/each}
		</ul>
	</nav>
{/if}
