<template>
    <article class="prose max-w-none relative dark:prose-invert prose-pre:bg-white dark:prose-pre:bg-gray-800 prose-pre:text-gray-900 dark:prose-pre:text-gray-300">
        <ContentDoc>
            <template #not-found>
                <h1>Document not found <span class="text-main">(404)</span></h1>
                <p>This blog post could not be found.</p>
            </template>
            <template v-slot="{ doc }">
                <div class="lg:grid lg:grid-cols-6 gap-16 flex flex-col-reverse">
                    <div :class="{'lg:col-span-4': doc.toc, 'lg:col-span-6': !doc.toc}">
                        <ContentRenderer :value="doc" />
                    </div>
                    <div class="lg:col-span-2 not-prose" v-if="doc.toc">
                        <aside class="sticky top-8">
                            <div class="font-semibold mb-2">
                                Table of Contents
                            </div>
                            <nav>
                                <TocLinks :activeId="activeId" :links="doc.body.toc.links" :active-id="activeId"/>
                            </nav>
                        </aside>
                    </div>
                </div>
            </template>
        </ContentDoc>
    </article>
</template>

<script setup>
const activeId = ref(null);

onMounted(() => {
    let elements = [];

    const cb = (entries) => {
        for (const entry of entries) {
            if (entry.isIntersecting) {
                activeId.value = entry.target.id;
                break;
            }
        }
    };
    const observer = new IntersectionObserver(cb, {
        root: null,
        threshold: 0.5,
    });

    setTimeout(() => {
        elements = document.querySelectorAll('h2, h3');
        for (const element of elements) {
            observer.observe(element);
        }
    }, 150);
    onBeforeUnmount(() => {
        for (const element of elements) {
            observer.unobserve(element);
        }
    })
});
</script>
