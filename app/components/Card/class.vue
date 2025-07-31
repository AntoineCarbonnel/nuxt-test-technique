<script setup lang="ts">
import { ref, computed } from 'vue'
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
  <div class="max-w-2xl mx-auto p-6">
    <div class="bg-white rounded-xl shadow-md overflow-hidden">
      <div v-if="isEditing" class="p-6">
        <div class="flex justify-between items-start mb-6">
          <h2 class="text-2xl font-bold">En quelle classe es-tu ?</h2>
          <button 
            @click="isEditing = false"
            class="text-gray-400 hover:text-gray-600 transition-colors"
          >
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
        
        <div class="mb-6">
          <div class="grid grid-cols-3 gap-4">
            <template v-for="classe in classes" :key="classe">
              <button
                @click="selectedClass = classe"
                :class="[
                  'p-4 rounded-lg border-2 transition-all',
                  selectedClass === classe
                    ? 'border-black bg-black text-white'
                    : 'border-gray-200 hover:border-gray-400'
                ]"
              >
                {{ classe }}
              </button>
            </template>
          </div>
        </div>

        <hr class="my-6 border-gray-200">

        <div class="mb-6">
          <div class="grid grid-cols-1 gap-4">
            <template v-for="bac in bacs" :key="bac">
              <button
                @click="selectedBac = bac"
                :class="[
                  'p-4 rounded-lg border-2 text-left transition-all',
                  selectedBac === bac
                    ? 'border-black bg-black text-white'
                    : 'border-gray-200 hover:border-gray-400'
                ]"
              >
                {{ bac }}
              </button>
            </template>
          </div>
        </div>

        <button
          @click="handleSubmit"
          :disabled="!isFormValid"
          :class="[
            'w-full py-3 px-6 rounded-lg transition-all',
            isFormValid
              ? 'bg-black text-white hover:bg-gray-800'
              : 'bg-gray-200 text-gray-500 cursor-not-allowed'
          ]"
        >
          Confirmer
        </button>
      </div>

      <!-- Mode consultation -->
      <div v-else class="p-4">
        <div class="flex justify-between items-start">
          <div>
            <p class="text-sm text-gray-500 mb-1">Classe</p>
            <div class="space-y-1">
              <p class="font-medium">{{ selectedClass }}</p>
              <p class="font-medium">{{ selectedBac }}</p>
            </div>
          </div>
          <button 
            @click="handleEdit"
            class="text-gray-400 hover:text-gray-600 transition-colors"
          >
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
            </svg>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: all 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>