<script setup lang="ts">
import type { Content } from "@prismicio/client";
import ScrollTrigger from "gsap/dist/ScrollTrigger";
import gsap from "gsap";

// The array passed to `getSliceComponentProps` is purely optional.
// Consider it as a visual hint for you when templating your slice.
defineProps(
  getSliceComponentProps<Content.ShowcaseSlice>([
    "slice",
    "index",
    "slices",
    "context",
  ]),
);

onMounted(() => {
	const preferredReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)").matches;

	if (preferredReducedMotion) return;

	gsap.registerPlugin(ScrollTrigger);

	gsap.fromTo(
		".showcase__heading",
		{
			y: 100,
		},
		{
			y: 0,
			ease: "power2.inOut",
			duration: 1,
			scrollTrigger: {
				trigger: ".showcase__heading",
				start: "top bottom-=40%",
				toggleActions: "play pause resume reverse",
			},
		}
	);

	gsap.fromTo(
		".showcase__glow",
		{ 
			scale: 0.7,
			opacity: 0.1 
		},
		{ 
			scale: 1,
			opacity: 1,
			ease: "power2.inOut",
			duration: 1,
			scrollTrigger: {
				trigger: ".showcase__heading",
				start: "top bottom-=40%",
				toggleActions: "play pause resume reverse",
			},
		}
	);
});
</script>

<template>
  <Bounded
    :data-slice-type="slice.slice_type"
    :data-slice-variation="slice.variation"
  >
	<div class="showcase__glow absolute -z-10 aspect-video w-full max-w-2xl rounded-full bg-sky-700 
	blur-[120px] filter mix-blend-screen"></div>
	<PrismicRichText 
		:field="slice.primary.heading"
		class="showcase__heading text-balance text-center text-5xl font-medium md:text-7xl"
		wrapper="header"
	/>
	<article class="relative mt-16 grid items-center gap-8 rounded-xl border border-sky-50/20 bg-gradient-to-b from-gray-50/15 
	to-gray-50/5 p-8 backdrop-blur-sm lg:grid-cols-3 lg:gap-0 lg:py-12">
		<div class="gridBackground"></div>
		<div>
			<figure v-if="slice.primary.icon" class="flex w-fit items-center justify-center rounded-lg bg-sky-900 p-4 text-3xl">
				<Icon :name="slice.primary.icon"/>
			</figure>
			<PrismicText :field="slice.primary.subheading" wrapper="h3" class="mt-6 text-2xl font-normal" />
			<PrismicRichText :field="slice.primary.body" wrapper="div" class="prose prose-invert mt-4 max-w-xl" />
			<PrismicLink :field="slice.primary.cta" class="buttonLink mt-6" />
		</div>
		<PrismicImage 
		:field="slice.primary.image" 
		class="opacity-90 shadow-2xl lg:col-span-2 lg:pt-0"
		:class="slice.variation === 'reversed' ? 'lg:order-1 lg:translate-x-[15%]' : 'lg:-order-1 lg:translate-x-[-15%]'"
		/>
	</article>
  </Bounded>
</template>

<style scoped>
.gridBackground {
	background-image: url("/assets/grid-pattern.png");
	position: absolute;
	inset: 0;
	background-repeat: repeat;
	z-index: -1;
	background-position: center;
	opacity: 0.15;
	mask-image: radial-gradient(circle at 60% 50%, black 10%, transparent 40%);
}
</style>