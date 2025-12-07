<script setup lang="ts">
import { formData } from '../composables/useForm'
</script>

<template>
  <div class="flex flex-col gap-4">
    <h2 class="text-2xl font-bold text-primary">Finishing up</h2>
    <p class="text-gray-500 mb-4">Double-check everything looks OK before confirming.</p>

    <div class="bg-base-200 rounded-lg p-4">
      <div class="flex justify-between items-center border-b border-gray-300 pb-4">
        <div>
          <h3 class="font-bold capitalize">
            {{ formData.plan }} ({{ formData.billing }})
          </h3>
          <button class="text-sm text-primary underline hover:text-primary-focus">
            Change
          </button>
        </div>
        <div class="font-bold text-lg">
          $9/mo <!-- Logic for price would go here -->
        </div>
      </div>

      <div class="pt-4 space-y-2">
        <div class="flex justify-between text-sm text-gray-500">
          <span>Online service</span>
          <span class="text-gray-700">+$1/mo</span>
        </div>
        <div class="flex justify-between text-sm text-gray-500">
          <span>Larger storage</span>
          <span class="text-gray-700">+$2/mo</span>
        </div>
      </div>
    </div>

    <div class="flex justify-between items-center px-4 mt-4">
      <span class="text-gray-500">Total (per month)</span>
      <span class="text-xl font-bold text-primary">+$12/mo</span>
    </div>
  </div>
</template>
