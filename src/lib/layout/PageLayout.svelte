<script lang="ts">
	import FacebookIcon from '$lib/icons/FacebookIcon.svelte';
	import InstagramIcon from '$lib/icons/InstagramIcon.svelte';
	import VimeoIcon from '$lib/icons/VimeoIcon.svelte';
	import YoutubeIcon from '$lib/icons/YoutubeIcon.svelte';
	import { onMount } from 'svelte';
	import '../../app.css';
	import SectionLayout from './SectionLayout.svelte';
	import Tag from '$lib/components/Tag.svelte';
	import FacebookShareButton from '$lib/components/FacebookShareButton.svelte';
	import ShareButton from '$lib/components/ShareButton.svelte';
	import { page } from '$app/stores';
	import { browser } from '$app/environment';

	onMount(() => {
		console.log('Page Layout mounted');
	});
	export let title = 'OUR WORK';
	export let icon = '';
	export let description = 'WE ARE PROUD TO PRESENT';
	export let bgImage = '/images/headingBG.png';
	export let bgImageMobile = '/images/headingBG.png';
	export let bgColor = '';
	export let tagText = '';
	export let rightComp = false;
	export let className: string = '';
	export let renderTitleAsH1: boolean = false;
	let url: string = '';
	onMount(() => {
		if (typeof window !== 'undefined') {
			url = window.location.href;
		}
		if (bgImage == '') {
			bgImage = '/images/headingBG.png';
		}
	});
</script>

<div class={`bg-[${bgColor}] ${className} relative w-full`} class:min-h-[420px]={bgImage != ''}>
	<SectionLayout
		className="absolute top-1/2 left-1/2 -translate-y-1/2 -translate-x-1/2 !py-0 w-full"
	>
		{#if browser && !$page.url.href?.includes('blog')}
			<div class="flex flex-wrap md:flex-nowrap justify-start items-center">
				<div class="flex flex-col w-full justify-end items-start z-[1]">
					{#if description != ''}
						<p>{description}</p>
					{/if}
					{#if icon != ''}
						<img src={icon} alt={title} class="w-20 h-20 mt-4" />
					{/if}
					{#if renderTitleAsH1}
						<h1 class="text-left renderAsH1">{title}</h1>
					{:else}
						<h2 class="text-left">{title}</h2>
					{/if}
					{#if tagText != ''}
						<Tag text={tagText} />
					{/if}
				</div>
				{#if rightComp}
					<div
						class="flex flex-col items-start md:items-end w-full md:ml-auto mt-10 md:mt-0 text-left"
					>
						<!-- <img
						src="/images/hero-gradient.png"
						alt="hero-gradient"
						class="absolute top-0 md:-left-[150px] left-0 w-[200px] opacity-60 md:opacity-100 md:w-auto pointer-events-none z-[0]"
					/> -->
						<div class="flex flex-col gap-4 lg:items-end lg:justify-end">
							<p class="text-left">2023-ZERO DESIGN STUDIO</p>
							<span class="flex justify-start items-center gap-4">
								<ShareButton {title} siteTitle={'Zero Design Studio'} {url} />
								<FacebookShareButton {url} />
								<!-- <InstagramIcon />
							<VimeoIcon />
							<YoutubeIcon /> -->
							</span>
						</div>
					</div>
				{/if}
			</div>
		{/if}
	</SectionLayout>
	<!-- <div
		class="absolute z-[-1] w-full bg-cover !bg-center bg-no-repeat xl:!bg-right h-[300px] md:h-[420px] top-0 left-0"
		style={`background-image:url(${bgImage});`}
	/> -->
	{#if bgImage != ''}
		<!-- <img src={bgImage} alt={'page-bg'} class="w-full" srcset="{bgImageMobile} 500w, " /> -->
		<picture class="block w-full">
			<source media="(max-width: 499px)" srcset={bgImageMobile} />
			<source media="(min-width: 500px)" srcset={bgImage} />
			<img src={bgImage} alt="page-bg" class="w-full" />
		</picture>
	{/if}
</div>
{#if browser && $page.url.href?.includes('blog')}
	<SectionLayout
		className="flex flex-col sm:flex-row justify-between items-start"
		padding="py-4 sm:py-10"
	>
		<div class="flex flex-col w-full justify-end items-start z-[1] flex-1">
			{#if description != ''}
				<p>{description}</p>
			{/if}
			{#if icon != ''}
				<img src={icon} alt={title} class="w-20 h-20 mt-4" />
			{/if}
			{#if renderTitleAsH1}
				<h1 class="text-left renderAsH1 w-full">{title}</h1>
			{:else}
				<h2 class="text-left w-full">{title}</h2>
			{/if}
			<!-- <h2 class="text-left">{title}</h2> -->
			{#if tagText != ''}
				<Tag text={tagText} />
			{/if}
		</div>
		{#if rightComp}
			<div class="flex flex-col items-start md:items-end mt-10 md:mt-0 text-left min-w-[300px]">
				<!-- <img
						src="/images/hero-gradient.png"
						alt="hero-gradient"
						class="absolute top-0 md:-left-[150px] left-0 w-[200px] opacity-60 md:opacity-100 md:w-auto pointer-events-none z-[0]"
					/> -->
				<div class="flex flex-col gap-4 lg:items-end lg:justify-end">
					<p class="text-left">2023-ZERO DESIGN STUDIO</p>
					<span class="flex justify-start items-center gap-4">
						<ShareButton {title} siteTitle={'Zero Design Studio'} {url} />
						<FacebookShareButton {url} />
						<!-- <InstagramIcon />
							<VimeoIcon />
							<YoutubeIcon /> -->
					</span>
				</div>
			</div>
		{/if}
	</SectionLayout>
{/if}
<slot />
