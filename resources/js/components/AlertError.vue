<script setup lang="ts">
import { AlertCircle } from '@lucide/vue';
import { useLang } from '@erag/lang-sync-inertia/vue';
import { computed } from 'vue';
import { Alert, AlertDescription, AlertTitle } from '@/components/ui/alert';

const { __ } = useLang();

const props = defineProps<{
    errors: string[];
    title?: string;
}>();

const uniqueErrors = computed(() => Array.from(new Set(props.errors)));
const displayTitle = computed(() => props.title ?? __('Something went wrong.'));
</script>

<template>
    <Alert variant="destructive">
        <AlertCircle class="size-4" />
        <AlertTitle>{{ displayTitle }}</AlertTitle>
        <AlertDescription>
            <ul class="list-inside list-disc text-sm">
                <li v-for="(error, index) in uniqueErrors" :key="index">
                    {{ error }}
                </li>
            </ul>
        </AlertDescription>
    </Alert>
</template>
