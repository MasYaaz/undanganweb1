<!-- src/lib/components/Navbar.svelte -->
<script lang="ts">
	import { FontAwesomeIcon } from '@fortawesome/svelte-fontawesome';
	import {
		faPerson,
		faPersonDress,
		faCalendarCheck,
		faImage,
		faRectangleList
	} from '@fortawesome/free-solid-svg-icons';
	export let show = true; // dikontrol dari luar

	// Fungsi scroll ke ID tertentu
	function scrollToSection(id: string) {
		const section = document.getElementById(id);
		if (section) {
			section.scrollIntoView({ behavior: 'smooth' });
		}
	}
</script>

{#if show}
	<nav
		class="fixed top-0 z-50 flex w-full items-center justify-center bg-white/30 px-6 py-4 shadow backdrop-blur-md"
	>
		<h1 class="text-lg font-bold">Undangan Kami</h1>
	</nav>
	<nav
		class="fixed bottom-0 z-50 flex w-full items-center justify-center bg-white/30 px-6 py-4 shadow backdrop-blur-md"
	>
		<ul class="flex gap-6 text-center text-sm">
			<li>
				<button
					on:click={() => scrollToSection('section2')}
					class="flex flex-col items-center transition-transform duration-300 hover:scale-105 hover:cursor-pointer"
				>
					<div class="flex">
						<FontAwesomeIcon icon={faPerson} class="fa-2x" />
						<FontAwesomeIcon icon={faPersonDress} class="fa-2x text-red-300" />
					</div>
					<span class="mt-1 uppercase font-primary font-bold text-[6px]">Mempelai</span>
				</button>
			</li>
			<li>
				<button
					on:click={() => scrollToSection('section3')}
					class="flex flex-col items-center transition-transform duration-300 hover:scale-105 hover:cursor-pointer"
				>
					<FontAwesomeIcon icon={faCalendarCheck} class="fa-2x" />
					<span class="mt-1 uppercase font-primary font-bold text-[6px]">Acara</span>
				</button>
			</li>
			<li>
				<button
					on:click={() => scrollToSection('section4')}
					class="flex flex-col items-center transition-transform duration-300 hover:scale-105 hover:cursor-pointer"
				>
					<FontAwesomeIcon icon={faImage} class="fa-2x" />
					<span class="mt-1 uppercase font-primary font-bold text-[6px]">Galeri</span>
				</button>
			</li>
			<li>
				<button
					on:click={() => scrollToSection('section5')}
					class="flex flex-col items-center transition-transform duration-300 hover:scale-105 hover:cursor-pointer"
				>
					<FontAwesomeIcon icon={faRectangleList} class="fa-2x md:fa-3x" />
					<span class="mt-1 uppercase font-primary font-bold text-[6px] md:text-[8px]">Ucapan</span>
				</button>
			</li>
		</ul>
	</nav>
{/if}
