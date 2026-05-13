<script lang="ts">
	import { branding } from '$lib/stores';
	import { getContext } from 'svelte';

	const i18n = getContext('i18n');
</script>

<div class="flex flex-col h-full justify-between text-sm">
	<div class="overflow-y-scroll max-h-[28rem] md:max-h-full space-y-4">
		<div class="mb-2 text-sm font-medium flex items-center gap-2">
			<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16" fill="currentColor" class="size-3.5 text-gray-400">
				<path fill-rule="evenodd" d="M8 1a3.5 3.5 0 0 0-3.5 3.5V5A2.5 2.5 0 0 0 2 7.5v4A2.5 2.5 0 0 0 4.5 14h7A2.5 2.5 0 0 0 14 11.5v-4A2.5 2.5 0 0 0 11.5 5v-.5A3.5 3.5 0 0 0 8 1Zm2.5 4v-.5a2.5 2.5 0 0 0-5 0V5h5Z" clip-rule="evenodd"/>
			</svg>
			{$i18n.t('Branding')}
		</div>

		<div class="space-y-3">
			<div class="flex w-full justify-between items-center">
				<div class="text-xs font-medium">{$i18n.t('Favicon URL')}</div>
				<div class="text-xs text-gray-500 break-all max-w-[60%] text-right">
					{$branding?.favicon_url || $i18n.t('Not set')}
				</div>
			</div>

			<div class="flex w-full justify-between items-center">
				<div class="text-xs font-medium">{$i18n.t('Logo URL')}</div>
				<div class="text-xs text-gray-500 break-all max-w-[60%] text-right">
					{$branding?.logo_url || $i18n.t('Not set')}
				</div>
			</div>

			<div class="flex w-full justify-between items-center">
				<div class="text-xs font-medium">{$i18n.t('Logo Dark URL')}</div>
				<div class="text-xs text-gray-500 break-all max-w-[60%] text-right">
					{$branding?.logo_dark_url || $i18n.t('Not set')}
				</div>
			</div>

			<div class="flex w-full justify-between items-center">
				<div class="text-xs font-medium">{$i18n.t('Default Background Image URL')}</div>
				<div class="text-xs text-gray-500 break-all max-w-[60%] text-right">
					{$branding?.default_background_image_url || $i18n.t('Not set')}
				</div>
			</div>

			<div class="flex w-full justify-between items-center">
				<div class="text-xs font-medium">{$i18n.t('Primary Color')}</div>
				<div class="flex items-center gap-2">
					{#if $branding?.primary_color}
						<div
							class="size-4 rounded-full border border-gray-300"
							style="background-color: {$branding.primary_color}"
						></div>
					{/if}
					<div class="text-xs text-gray-500">
						{$branding?.primary_color || $i18n.t('Not set')}
					</div>
				</div>
			</div>

			<div class="flex w-full justify-between items-center">
				<div class="text-xs font-medium">{$i18n.t('Accent Color')}</div>
				<div class="flex items-center gap-2">
					{#if $branding?.accent_color}
						<div
							class="size-4 rounded-full border border-gray-300"
							style="background-color: {$branding.accent_color}"
						></div>
					{/if}
					<div class="text-xs text-gray-500">
						{$branding?.accent_color || $i18n.t('Not set')}
					</div>
				</div>
			</div>
		</div>

		<div class="mt-4 text-xs text-gray-400 italic space-y-1">
			<div>{$i18n.t('Branding values are configured via environment variables on the server.')}</div>
			<div class="font-mono">WEBUI_FAVICON_URL, WEBUI_LOGO_URL, WEBUI_LOGO_DARK_URL</div>
			<div class="font-mono">WEBUI_DEFAULT_BACKGROUND_IMAGE_URL, WEBUI_PRIMARY_COLOR, WEBUI_ACCENT_COLOR</div>
			<div class="mt-2">
				{$i18n.t('Brand colors can be used in custom CSS with')}
				<span class="font-mono">var(--brand-primary)</span>
				{$i18n.t('and')}
				<span class="font-mono">var(--brand-accent)</span>.
			</div>
		</div>
	</div>
</div>
