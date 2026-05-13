<script lang="ts">
	import { branding } from '$lib/stores';
	import { WEBUI_BASE_URL } from '$lib/constants';
	import { onMount } from 'svelte';

	export let size: string = 'size-6';
	export let className: string = '';
	export let fallback: string = `${WEBUI_BASE_URL}/static/favicon.png`;

	let imgSrc: string;
	let isDark = false;

	const darkQuery =
		typeof window !== 'undefined' ? window.matchMedia('(prefers-color-scheme: dark)') : null;

	const updateSrc = () => {
		isDark =
			document.documentElement.classList.contains('dark') ||
			(document.documentElement.classList.contains('light')
				? false
				: darkQuery?.matches ?? false);

		const logoUrl = $branding?.logo_url || '';
		const logoDarkUrl = $branding?.logo_dark_url || '';

		if (isDark && logoDarkUrl) {
			imgSrc = logoDarkUrl;
		} else if (logoUrl) {
			imgSrc = logoUrl;
		} else {
			imgSrc = fallback;
		}
	};

	const onError = (e: Event) => {
		(e.target as HTMLImageElement).src = fallback;
	};

	onMount(() => {
		updateSrc();
		if (darkQuery) {
			darkQuery.addEventListener('change', updateSrc);
		}
		const observer = new MutationObserver(updateSrc);
		observer.observe(document.documentElement, { attributes: true, attributeFilter: ['class'] });
		return () => {
			if (darkQuery) {
				darkQuery.removeEventListener('change', updateSrc);
			}
			observer.disconnect();
		};
	});

	$: if ($branding) {
		updateSrc();
	}
</script>

<img
	src={imgSrc || fallback}
	class={[size, className].filter(Boolean).join(' ')}
	alt="logo"
	on:error={onError}
/>
