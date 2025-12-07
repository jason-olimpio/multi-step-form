<script setup lang="ts">
import { formData } from '../composables/useForm'
</script>

<template>
  <div class="flex flex-col gap-4 items-center justify-center">
    <div class="text-center mb-6">
      <div class="inline-flex items-center justify-center w-16 h-16 bg-primary rounded-full mb-4">
        <img src="/images/icon-thank-you.svg" alt="Thank you" class="w-8 h-8" />
      </div>
      <h2 class="text-3xl font-bold text-primary mb-2">Thank you!</h2>
      <p class="text-gray-500">
        Thanks for confirming your subscription. We hope you have fun using our platform. If you ever need support, please feel free to email us at support@loremgaming.com.
      </p>
    </div>

    <div class="w-full bg-base-200 rounded-lg p-6 mt-6">
      <h3 class="font-bold text-lg mb-4">Order Summary</h3>
      
      <div class="space-y-3 border-b border-gray-300 pb-4">
        <div class="flex justify-between">
          <span class="capitalize">{{ formData.plan }} ({{ formData.billing }})</span>
          <span class="font-bold">$9/mo</span>
        </div>
        <div class="flex justify-between text-sm text-gray-500">
          <span>Online service</span>
          <span>+$1/mo</span>
        </div>
        <div class="flex justify-between text-sm text-gray-500">
          <span>Larger storage</span>
          <span>+$2/mo</span>
        </div>
      </div>

      <div class="flex justify-between items-center pt-4 mt-4">
        <span class="text-gray-600">Total (per month)</span>
        <span class="text-2xl font-bold text-primary">+$12/mo</span>
      </div>
    </div>
  </div>
</template>
