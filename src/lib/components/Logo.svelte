<script lang="ts">
	import { commonStore } from '$lib/stores/commons.store';
	import { homeStore } from '$lib/stores/hero.store';
	import { getImageUrl } from '$lib/utils/functions';
	import { createEventDispatcher, onMount } from 'svelte';

	export let url: string = '/logo.png';
	export let title: string = '';
	export let subTitle: string = '';

	const dispatch = createEventDispatcher();

	function onClick() {
		dispatch('click');
	}

	onMount(() => {
		url = getImageUrl($commonStore.header.Logo);
	});
</script>

<div
	class="flex justify-center items-center gap-2 max-w-[200px]"
	on:click={onClick}
	tabindex="0"
	role="button"
	on:keydown={(e) => {
		if (e.key === 'Enter') {
			onClick();
		}
	}}
>
	<img
		src={url}
		alt="Logo - Zero Design Studios"
		class={'w-14 h-13 sm:w-16 sm:h-15 md:w-20 md:h-18'}
	/>
	<div class="flex flex-col align-stretch">
		{#if title?.length > 0}
			<p
				class="block text-[1.5rem] sm:text-[1.8rem] md:text-[2.5rem] font-bold leading-8 md:leading-10"
			>
				{title}
			</p>
		{/if}
		{#if subTitle?.length > 0}
			<p class="text-[0.5rem] sm:text-[0.6rem] md:text-sm">{subTitle}</p>
		{/if}
	</div>
</div>
