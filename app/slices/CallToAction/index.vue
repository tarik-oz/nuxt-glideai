<script setup lang="ts">
import type { Content } from "@prismicio/client";
import Bounded from "~/components/Bounded.vue";

// The array passed to `getSliceComponentProps` is purely optional.
// Consider it as a visual hint for you when templating your slice.
defineProps(
  getSliceComponentProps<Content.CallToActionSlice>([
    "slice",
    "index",
    "slices",
    "context",
  ]),
);
</script>

<template>
  <Bounded
    :data-slice-type="slice.slice_type"
    :data-slice-variation="slice.variation"
	class="py-32 md:py-40"
  >
	<div class="glow absolute -z-10 aspect-square w-full max-w-sm rounded-full bg-sky-500/50 blur-[160px] filter" />
	<div class="glassContainer rounded-lg bg-gradient-to-b from-gray-800 to-gray-900 p-4 md:rounded-xl">
		<GlideIcon class="w-24 h-24" />
	</div>
	<PrismicText :field="slice.primary.heading" wrapper="h2" class="mt-8 max-w-xl font-medium text-balance text-center text-5xl" />
	<div class="mt-6 flex gap-8 flex-wrap">
  		<PrismicLink 
			v-for="link in slice.primary.ctas" 
			:key="link.key"
			:field="link" 
			class="buttonLink"
		/>
    </div>
  </Bounded>
</template>
