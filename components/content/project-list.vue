<template>
    <div class="not-prose">
        <section v-if="pending">Loading...</section>
        <section v-else-if="error">Something went wrong</section>
        <section v-else>
            <ul class="grid grid-cols-1 gap-4">
                <li v-for="project in repos" :key="project.id" class="border border-gray-200 rounded-sm p-4 hover:bg-gray-100 dark:hover:bg-gray-800 font-mono">
                    <a :href="project.html_url" target="_blank">
                        <div class="flex items-center justify-between text-sm">
                            <div class="font-semibold">
                                {{ project.name }}
                            </div>
                            <div>{{ project.stargazers_count }} *</div>
                        </div>
                        <p>{{ project.description }}</p>
                    </a>
                </li>
            </ul>
        </section>
    </div>
</template>

<script setup>
    const { data, pending, error } = await useFetch('https://api.github.com/users/mihailtudos/repos');
    const repos = computed(() => {
        return data.value.filter(project => project.description?.length > 0).sort((a, b) => b.stargazers_count - a.stargazers_count)
    })
</script>

<style scoped>

</style>