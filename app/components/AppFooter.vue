<script lang="ts" setup>
import type { Content } from '@prismicio/client'

defineProps<{
    settings?: Content.SettingsDocument
}>()
</script>

<template>
    <footer>
        <nav aria-label="Footer" class="flex flex-col items-center justify-between gap-6 px-8 py-7 md:flex-row border-t border-gray-600">
            <NuxtLink to="/" class="z-50">
                <GlideLogo />
                <span class="sr-only">{{ settings?.data.site_title }} home page</span>
            </NuxtLink>

            
            <ul class="flex gap-6">
                <li v-for="link in settings?.data.navigation" :key="link.key">
                    <PrismicLink 
                    :field="link" 
                    class="inline-flex items-center min-h-11"
                    />
                </li>
            </ul>

        </nav>
    </footer>
</template>