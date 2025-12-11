<script setup lang="ts">
const baseUrl = import.meta.env.BASE_URL
const thankYouIcon = `${baseUrl}images/icon-thank-you.svg`
</script>

<template>
    <div class="text-center py-10 flex flex-col items-center gap-4">
        <img class="h-16 w-16" :src="thankYouIcon" />

        <h2 class="text-3xl font-bold text-primary">Thank you!</h2>

        <p class="text-gray-500">Thanks for confirming your subscription!
            We hope you have fun using our platform. If you ever need support, please
            feel free to email us at support@loremipsum.com.</p>
    </div>
</template>
