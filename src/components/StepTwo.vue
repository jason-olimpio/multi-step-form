<script setup lang="ts">
import { formData } from '../composables/useForm'

const plans = [
    { id: 'arcade', name: 'Arcade', price: '$9/mo', icon: '🕹️' },
    { id: 'advanced', name: 'Advanced', price: '$12/mo', icon: '🎮' },
    { id: 'pro', name: 'Pro', price: '$15/mo', icon: '🕹️' },
]
</script>

<template>
    <div class="flex flex-col gap-4">
        <h2 class="text-2xl font-bold text-primary">Select your plan</h2>
        <p class="text-gray-500 mb-4">You have the option of monthly or yearly billing.</p>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
            <div v-for="plan in plans" :key="plan.id"
                class="card border-2 cursor-pointer transition-all hover:border-primary"
                :class="formData.plan === plan.id ? 'border-primary bg-base-200' : 'border-base-300'"
                @click="formData.plan = plan.id">
                <div class="card-body p-4">
                    <span class="text-3xl mb-4">{{ plan.icon }}</span>
                    <h3 class="font-bold text-lg">{{ plan.name }}</h3>
                    <p class="text-sm text-gray-500">{{ plan.price }}</p>
                </div>
            </div>
        </div>

        <div class="form-control mt-6 bg-base-200 p-3 rounded-lg flex-row justify-center gap-4">
            <span :class="{ 'font-bold': formData.billing === 'monthly' }">Monthly</span>
            <input type="checkbox" class="toggle toggle-primary" :checked="formData.billing === 'yearly'"
                @change="formData.billing = formData.billing === 'monthly' ? 'yearly' : 'monthly'" />
            <span :class="{ 'font-bold': formData.billing === 'yearly' }">Yearly</span>
        </div>
    </div>
</template>
