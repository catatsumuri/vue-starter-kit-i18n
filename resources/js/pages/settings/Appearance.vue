<script setup lang="ts">
import { Head, setLayoutProps } from '@inertiajs/vue3';
import { useLang } from '@erag/lang-sync-inertia/vue';
import AppearanceTabs from '@/components/AppearanceTabs.vue';
import Heading from '@/components/Heading.vue';
import { edit } from '@/routes/appearance';

const { __ } = useLang();

setLayoutProps({
    breadcrumbs: [
        {
            title: __('Appearance settings'),
            href: edit(),
        },
    ],
});
</script>

<template>
    <Head :title="__('Appearance settings')" />

    <h1 class="sr-only">{{ __('Appearance settings') }}</h1>

    <div class="space-y-6">
        <Heading
            variant="small"
            :title="__('Appearance settings')"
            :description="__('Update the appearance settings for your account')"
        />
        <AppearanceTabs />
    </div>
</template>
