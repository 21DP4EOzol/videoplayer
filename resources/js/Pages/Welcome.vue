<script setup>
import { Head, Link } from '@inertiajs/vue3';
import NavLayout from '@/Layouts/NavLayout.vue';
import VideoCard from '@/Components/VideoCard.vue';

defineProps({
    videos: Array
});

function handleImageError() {
    document.getElementById('screenshot-container')?.classList.add('!hidden');
    document.getElementById('docs-card')?.classList.add('!row-span-1');
    document.getElementById('docs-card-content')?.classList.add('!flex-row');
    document.getElementById('background')?.classList.add('!hidden');
}
</script>

<template>
    <Head title="Youtube" />

    <NavLayout>
        <div class="grid 2xl:grid-cols-5 xl:grid-cols-4 lg:grid-cols-3 md:grid-cols-3 sm:grid-cols-2">
            
            <div v-for="video, index in videos" :key="video">
                <Link :href="route('video.show', {id: video.id})">
                    <VideoCard
                        :title="video.title"
                        :user="video.user"
                        :views="video.views"
                        :image="`https://picsum.photos/id/${index}/100`"
                        :videoUrl="video.video"
                        :thumbnail="video.thumbnail"
            />
                </Link>
            </div>
        </div>
    </NavLayout>

</template>
    

    