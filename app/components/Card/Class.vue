<script lang="ts" setup>
import {computed, ref} from 'vue'
import sectionData from '~/data/section.json'
import bacData from '~/data/bac.json'

const classes = Object.values(sectionData.classes).map(classe => classe.nom)
const bacs = Object.values(bacData.bac).map(type => type.nom)

const selectedClass = ref('')
const selectedBac = ref('')
const isEditing = ref(true)

const isFormValid = computed(() => {
	return selectedClass.value && selectedBac.value
})

const isFormEmpty = computed(() => {
	return !selectedClass.value && !selectedBac.value
})


const handleSubmit = () => {
	if (isFormValid.value) {
		isEditing.value = false
	}
}

const handleEdit = () => {
	isEditing.value = true
}
</script>

<template>
	<div class="bg-white rounded-2xl overflow-hidden">
		<div v-if="isEditing" class="p-6">
			<div class="flex justify-between items-start mb-6">
				<h2 class="font-bold">En quelle classe es-tu ?</h2>
				<button
						class="text-gray-400 hover:text-gray-600 transition-colors"
						@click="isEditing = false"
				>
					<svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 20 20" fill="none">
						<path d="M6.50491 13.4951L10 10M13.4951 6.50491L10 10M10 10L6.50491 6.50491M10 10L13.4951 13.4951" stroke="#1B1B1B" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
					</svg>
				</button>
			</div>

			<div class="mb-6">
				<div class="flex flex-wrap gap-2 rounded-3">
					<template v-for="classe in classes" :key="classe">
						<button
								:class="[
									'px-4 py-2 rounded-3xl border-2 transition-all',
									selectedClass === classe
										? 'bg-white border-black'
										: 'bg-[#F7F3F0] border-transparent'
								]"
								@click="selectedClass = classe"
						>
							{{ classe }}
						</button>
					</template>
				</div>
			</div>

			<hr class="my-6 border-gray-200">

			<div class="mb-6">
				<div class="flex flex-wrap gap-2 rounded-3">
					<template v-for="bac in bacs" :key="bac">
						<button
								:class="[
									'px-4 py-2 rounded-3xl border-2 transition-all',
                  selectedBac === bac
										? 'bg-white border-black'
										: 'bg-[#F7F3F0] border-transparent'
                ]"
								@click="selectedBac = bac"
						>
							{{ bac }}
						</button>
					</template>
				</div>
			</div>

			<button
					:class="[
						'w-full px-4 py-2 rounded-3xl border transition-all',
						isFormValid
							? 'bg-black text-white border-transparent'
							: 'bg-white text-gray-400 border-gray-200'
					]"
					:disabled="!isFormValid"
					@click="handleSubmit"
			>
				Confirmer
			</button>
		</div>

		<div v-else class="p-4">
			<div class="flex justify-between items-start">
				<div>
					<div class="flex flex-col gap-2 mb-1">
						<p :class="[
                'text-sm',
                isFormEmpty ? 'font-bold text-black' : 'text-gray-500'
              ]">
							Classe
						</p>
						<p v-if="isFormEmpty" class="text-sm text-gray-500">
							À compléter
						</p>
					</div>
					<div v-if="!isFormEmpty" class="flex gap-1">
						<p class="font-bold">{{ selectedClass }}</p>
						<p class="font-bold">{{ selectedBac }}</p>
					</div>
				</div>
				<button
						@click="handleEdit"
						class="text-gray-400 hover:text-gray-600 transition-colors"
				>
					<svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
						<path d="M2 14L8 14L14 14" stroke="#1B1B1B" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
						<path d="M8.14788 3.88559L10.0335 1.99997L13.3333 5.2998L11.4477 7.18542M8.14788 3.88559L4.50778 7.52569C4.32024 7.71323 4.21488 7.96758 4.21488 8.2328L4.21489 11.1184L7.1005 11.1184C7.36572 11.1184 7.62007 11.0131 7.80761 10.8255L11.4477 7.18542M8.14788 3.88559L11.4477 7.18542" stroke="#1B1B1B" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
					</svg>
				</button>
			</div>
		</div>
	</div>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
	transition: all 0.1s ease;
}

.fade-enter-from,
.fade-leave-to {
	opacity: 0;
	transform: translateY(-10px);
}
</style>