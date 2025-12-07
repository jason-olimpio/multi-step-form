<script setup lang="ts">
import { formData } from '../composables/useForm'
</script>

<template>
    <div class="flex flex-col gap-4">
        <h2 class="text-2xl font-bold text-primary">Personal Info</h2>
        <p class="text-gray-500 mb-4">Please provide your name, email address, and phone number.</p>

        <div class="form-control w-full">
            <label class="label">
                <span class="label-text">Name</span>
            </label>
            <input v-model="formData.name" type="text" placeholder="e.g. Stephen King"
                class="input input-bordered w-full" />
        </div>

        <div class="form-control w-full">
            <label class="label">
                <span class="label-text">Email Address</span>
            </label>
            <input v-model="formData.email" type="email" placeholder="e.g. stephenking@lorem.com"
                class="input input-bordered w-full" />
        </div>

        <div class="form-control w-full">
            <label class="label">
                <span class="label-text">Phone Number</span>
            </label>
            <input v-model="formData.phone" type="tel" placeholder="e.g. +1 234 567 890"
                class="input input-bordered w-full" />
        </div>
    </div>
</template>
