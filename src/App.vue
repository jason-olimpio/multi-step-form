<script setup lang="ts">
import { ref, computed } from 'vue'
import { StepOne, StepTwo, StepThree, StepFour, ThankYou } from './components'
import { validateStep } from './composables/useForm'

const steps = ['Your Info', 'Select Plan', 'Add-ons', 'Summary']
const currentStepIndex = ref(0)
const submitted = ref(false)

const baseUrl = import.meta.env.BASE_URL
const desktopSidebarBg = `url(${baseUrl}images/bg-sidebar-desktop.svg)`
const mobileSidebarBg = `url(${baseUrl}images/bg-sidebar-mobile.svg)`

const currentStepComponent = computed(() => {
  if (submitted.value) return ThankYou

  switch (currentStepIndex.value) {
    case 0: return StepOne
    case 1: return StepTwo
    case 2: return StepThree
    case 3: return StepFour
    default: return StepOne
  }
})

const handleSubmit = () => {
  const action = currentStepIndex.value < steps.length - 1
    ? goToNextStep
    : submitForm

  action()
}

const goToPreviousStep = () => {
  if (currentStepIndex.value > 0)
    currentStepIndex.value--
}

const goToNextStep = () => {
  const canAdvance = validateStep(currentStepIndex.value) && currentStepIndex.value < steps.length - 1

  if (canAdvance) currentStepIndex.value++
}

const goToStep = (stepIndex: number) => currentStepIndex.value = stepIndex

const submitForm = () => submitted.value = true
</script>

<template>
  <div :class="[
    'min-h-screen bg-gray-50 flex justify-center px-4 pt-0 pb-24 lg:p-10 lg:pb-10',
    submitted ? 'items-center' : 'items-start'
  ]">
    <div class="w-full max-w-4xl">
      <div class="w-screen relative left-1/2 right-1/2 -ml-[50vw] lg:hidden">
        <div class="h-40 w-full bg-cover bg-no-repeat flex items-center justify-center gap-4"
          :style="{ backgroundImage: mobileSidebarBg }">
          <div v-for="(_, index) in steps" :key="index" :class="[
            'w-8 h-8 rounded-full flex items-center justify-center font-bold text-sm',
            index === currentStepIndex ? 'bg-white text-blue-700' : 'border border-white text-white'
          ]">
            {{ index + 1 }}
          </div>
        </div>
      </div>

      <div class="card w-full bg-white shadow-xl overflow-hidden rounded-2xl
               relative -mt-8 lg:mt-0">
        <div class="card-body p-4 lg:p-6 flex flex-col lg:flex-row">
          <div class="bg-no-repeat rounded-lg p-8 flex-col min-w-[250px] hidden lg:flex"
            :style="{ backgroundImage: desktopSidebarBg }">
            <div class="space-y-8">
              <div v-for="(step, index) in steps" :key="index" class="flex items-center gap-4">
                <div :class="[
                  'w-8 h-8 rounded-full flex items-center justify-center font-bold text-md shrink-0',
                  index === currentStepIndex ? 'bg-white text-blue-700' : 'border'
                ]">
                  {{ index + 1 }}
                </div>

                <div class="uppercase">
                  <div class="text-xs">Step {{ index + 1 }}</div>
                  <div class="text-sm font-bold">{{ step }}</div>
                </div>
              </div>
            </div>
          </div>

          <div class="flex-1 lg:ml-10">
            <form @submit.prevent="handleSubmit" class="px-2 lg:px-0">
              <div class="min-h-[200px] py-4">
                <Transition name="fade" mode="out-in">
                  <component :is="currentStepComponent" @goToStep="goToStep" />
                </Transition>
              </div>

              <div v-if="!submitted" class="flex justify-between gap-4 mt-6
                       fixed bottom-0 left-0 right-0 bg-white px-4 py-4
                       lg:static lg:bg-transparent lg:px-0 lg:py-0">
                <button type="button"
                  class="px-4 py-2 text-gray-400 font-medium bg-transparent hover:text-gray-600 disabled:text-gray-300"
                  :disabled="currentStepIndex === 0" @click="goToPreviousStep">
                  Go Back
                </button>

                <button v-if="currentStepIndex < steps.length - 1" type="submit" class="btn btn-primary ml-auto">
                  Next Step
                </button>

                <button v-else type="submit" class="btn btn-primary ml-auto">
                  Confirm
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
