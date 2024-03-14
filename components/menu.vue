<script setup lang="ts">

</script>

<template>
    <nav class="font-mono">
        <ul class="flex flex-col md:flex-row gap-4">
            <li>
                <NuxtLink to="/" class="link">Home</NuxtLink>
            </li>
            <li>
                <NuxtLink to="/about" class="link">About</NuxtLink>
            </li>
            <li>
                <NuxtLink to="/projects" class="link">Projects</NuxtLink>
            </li>
            <li>
                <NuxtLink to="/blog" class="link">Blog</NuxtLink>
            </li>
        </ul>
    </nav>
</template>

<style scoped>
.link {
    @apply hover:bg-gray-100 p-2 dark:hover:!bg-gray-800 text-2xl md:text-base
}
</style>