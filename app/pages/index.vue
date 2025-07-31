<script lang="ts" setup>

</script>

<template>
	<section class="flex flex-col mx-6 my-8 max-w-2xl gap-y-4">
		<article class="rounded-3xl radient text-white p-4">
			<h1 class="font-bold text-lg">
				Lycée Gaston Berger
			</h1>
			<section class="flex gap-2 mt-2">
				<div class="flex gap-1 font-light">
					<img src="/assets/map-pin.png" alt="">
					Lille
				</div>
				<div class="flex gap-1 font-light">
					<img src="/assets/building.png" alt="">
					lycée public
				</div>
			</section>
			<section>
				<button class="bg-white rounded-full px-6 py-2 text-black mt-6">
					Modifier
				</button>
			</section>
		</article>
		<CardClass />
		<CardSpecialities />
		<CardNotes />
	</section>
</template>

<style>
.radient {
	background: #FF7342;
	background: linear-gradient(127deg, rgba(255, 115, 66, 1) 0%, rgba(219, 116, 153, 1) 78%, rgba(177, 118, 255, 1) 100%);
}
</style>