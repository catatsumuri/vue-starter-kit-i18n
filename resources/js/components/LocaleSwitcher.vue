<script setup lang="ts">
import { router, usePage } from '@inertiajs/vue3';
import { computed } from 'vue';
import {
    Select,
    SelectContent,
    SelectItem,
    SelectTrigger,
    SelectValue,
} from '@/components/ui/select';
import { switchMethod } from '@/routes/locale';

const page = usePage();
const locale = computed(() => page.props.locale);
const locales = computed(() => page.props.locales);

function handleChange(value: string) {
    router.post(switchMethod.url(), { locale: value }, { preserveScroll: true });
}
</script>

<template>
    <Select :model-value="locale" @update:model-value="handleChange">
        <SelectTrigger class="w-auto gap-2 text-xs">
            <SelectValue />
        </SelectTrigger>
        <SelectContent>
            <SelectItem
                v-for="(name, code) in locales"
                :key="code"
                :value="code"
                class="text-xs"
            >
                {{ name }}
            </SelectItem>
        </SelectContent>
    </Select>
</template>
