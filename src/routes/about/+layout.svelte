<script>
	import { onNavigate } from '$app/navigation';
	import CustomHead from '$lib/components/CustomHead.svelte';
	import DecorationLeft from '$lib/components/DecorationLeft.svelte';
	import PageLayout from '$lib/layout/PageLayout.svelte';
	import SectionLayout from '$lib/layout/SectionLayout.svelte';
	import AboutSection from '$lib/sections/AboutSection.svelte';
	import { getImageUrl } from '$lib/utils/functions';

	export let data;
	let { Page_Title, Page_Description, Bg_Image_File, About_Description } = data;
	let imgSrc = getImageUrl(Bg_Image_File.Image);
	let imgSrcMobile = getImageUrl(Bg_Image_File.mobileImage);

	onNavigate((navigation) => {
		// @ts-expect-error this is a sveltekit feature
		if (!document.startViewTransition) return;

		return new Promise((resolve) => {
			// @ts-expect-error this is a sveltekit feature
			document.startViewTransition(async () => {
				resolve();
				await navigation.complete;
			});
		});
	});
</script>

<CustomHead seo={data.seo} />
<PageLayout
	title={Page_Title}
	description={Page_Description}
	bgImage={imgSrc}
	bgImageMobile={imgSrcMobile}
>
	<!-- <SectionLayout className="py-[50px]"> -->
	<slot />
	<!-- </SectionLayout> -->
</PageLayout>
<DecorationLeft bottom={'90%'} />

<style>
	@keyframes fade-in {
		from {
			opacity: 0;
		}
	}

	@keyframes fade-out {
		to {
			opacity: 0;
		}
	}

	@keyframes slide-from-right {
		from {
			transform: translateX(30px);
		}
	}

	@keyframes slide-to-left {
		to {
			transform: translateX(-30px);
		}
	}

	:root::view-transition-old(root) {
		animation: 90ms cubic-bezier(0.4, 0, 1, 1) both fade-out,
			300ms cubic-bezier(0.4, 0, 0.2, 1) both slide-to-left;
	}

	:root::view-transition-new(root) {
		animation: 210ms cubic-bezier(0, 0, 0.2, 1) 90ms both fade-in,
			300ms cubic-bezier(0.4, 0, 0.2, 1) both slide-from-right;
	}
</style>
