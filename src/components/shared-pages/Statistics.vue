<template>
	<div class="flex items-center">
		<RouterLinkUp v-if="!advancedSettings" />
		<h1>
			{{ $t("skippedTime") }}
		</h1>
	</div>
	<div class="py-1 m-0 flex justify-between">
		<p>{{ $t("statisticAd", ["Amazon"]) }}</p>
		<p>{{ getTimeFormatted(settings.Statistics.AmazonAdTimeSkipped) }}</p>
	</div>
	<template v-if="advancedSettings">
		<p class="description">
			{{ $t("amazonAdDescription") }}
		</p>
		<hr />
	</template>
	<div class="py-1 m-0 flex justify-between">
		<p>{{ $t("statisticAd", ["Netflix"]) }}</p>
		<p>{{ getTimeFormatted(settings.Statistics.NetflixAdTimeSkipped) }}</p>
	</div>
	<template v-if="advancedSettings">
		<p class="description">
			{{ $t("netflixAdDescription") }}
		</p>
		<hr />
	</template>
	<div class="py-1 m-0 flex justify-between">
		<p>{{ $t("statisticAd", ["Disney"]) }}</p>
		<p>{{ getTimeFormatted(settings.Statistics.DisneyAdTimeSkipped) }}</p>
	</div>
	<template v-if="advancedSettings">
		<p class="description">
			{{ $t("disneyAdDescription") }}
		</p>
		<hr />
	</template>
	<div class="py-1 m-0 flex justify-between">
		<p>{{ $t("statisticIntro") }}</p>
		<p>{{ getTimeFormatted(settings.Statistics.IntroTimeSkipped) }}</p>
	</div>
	<template v-if="advancedSettings">
		<p class="description">
			{{ $t("statisticIntroDescription") }}
		</p>
		<hr />
	</template>
	<div class="py-1 m-0 flex justify-between">
		<p>{{ $t("statisticRecap") }}</p>
		<p>{{ getTimeFormatted(settings.Statistics.RecapTimeSkipped) }}</p>
	</div>
	<template v-if="advancedSettings">
		<p class="description">
			{{ $t("statisticskipRecapDescription") }}
		</p>
		<hr />
	</template>
	<div class="py-1 m-0 flex justify-between">
		<p>{{ $t("statisticSegments") }}</p>
		<p>{{ settings.Statistics.SegmentsSkipped }}</p>
	</div>
	<template v-if="advancedSettings">
		<p class="description">
			{{ $t("statisticSegmentsDescription") }}
		</p>
		<hr />
	</template>
</template>
<script setup lang="ts">
const optionsStore = useOptionsStore()
const { settings } = storeToRefs(optionsStore)

function getTimeFormatted(sec = 0) {
	if (typeof sec !== "number") return "0s"
	let days = Math.floor(sec / 86400)
	let hours = Math.floor((sec % 86400) / 3600)
	let minutes = Math.floor(((sec % 86400) % 3600) / 60)
	let seconds = Math.floor(((sec % 86400) % 3600) % 60)
	let text
	if (days > 0) text = `${days}d ${hours}h ${minutes}m`
	else if (hours > 0) text = `${hours}h ${minutes}m ${seconds}s`
	else if (minutes > 0) text = `${minutes}m ${seconds}s`
	else text = `${seconds}s`
	return text
}
const props = defineProps({
	advancedSettings: {
		type: Boolean,
		default: false,
	},
})
</script>
<style scoped></style>
