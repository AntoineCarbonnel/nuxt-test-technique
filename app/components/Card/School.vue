<script lang="ts" setup>
import { ref } from 'vue'
import schoolsData from '@/data/school.json'

interface School {
	nom: string
}

const schools = ref<School[]>(schoolsData.school)

const selectedSchool = ref<School>(schools.value[0])

const isEditing = ref(false)
const toggleEdit = () => {
	isEditing.value = !isEditing.value
}
</script>

<template>
	<article class="rounded-3xl radient text-white p-4">
		<div v-if="!isEditing">
			<h1 class="font-bold text-lg">
				{{ selectedSchool.nom }}
			</h1>
		</div>
		<div v-else>
			<select
					v-model="selectedSchool"
					class="w-full p-2 rounded appearance-none text-white border-0 focus:outline-none focus:ring-0 font-bold text-lg cursor-pointer bg-white/10 transition-colors"
			>
				<option
						v-for="school in schools"
						:key="school.nom"
						:value="school"
						class="bg-gray-800"
				>
					{{ school.nom }}
				</option>
			</select>

		</div>

		<section class="flex gap-2 mt-2">
			<div class="flex gap-1 font-light">
				<img src="/assets/map-pin.png" alt="">
				Lille
			</div>
			<div class="flex gap-1 font-light">
				<img src="/assets/building.png" alt="">
				Lycée public
			</div>
		</section>

		<section>
			<button
					@click="toggleEdit"
					class="bg-white rounded-full px-6 py-2 text-black mt-6"
			>
				{{ isEditing ? 'Valider' : 'Modifier' }}
			</button>
		</section>
	</article>
</template>