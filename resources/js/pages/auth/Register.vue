<script setup lang="ts">
import { Form, Head, setLayoutProps } from '@inertiajs/vue3';
import { useLang } from '@erag/lang-sync-inertia/vue';
import InputError from '@/components/InputError.vue';
import PasswordInput from '@/components/PasswordInput.vue';
import TextLink from '@/components/TextLink.vue';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Label } from '@/components/ui/label';
import { Spinner } from '@/components/ui/spinner';
import { login } from '@/routes';
import { store } from '@/routes/register';

const { __ } = useLang();

defineProps<{
    passwordRules: string;
}>();

setLayoutProps({
    title: __('Create an account'),
    description: __('Enter your details below to create your account'),
});
</script>

<template>
    <Head :title="__('Register')" />

    <Form
        v-bind="store.form()"
        :reset-on-success="['password', 'password_confirmation']"
        v-slot="{ errors, processing }"
        class="flex flex-col gap-6"
    >
        <div class="grid gap-6">
            <div class="grid gap-2">
                <Label for="name">{{ __('Name') }}</Label>
                <Input
                    id="name"
                    type="text"
                    required
                    autofocus
                    :tabindex="1"
                    autocomplete="name"
                    name="name"
                    :placeholder="__('Full name')"
                />
                <InputError :message="errors.name" />
            </div>

            <div class="grid gap-2">
                <Label for="email">{{ __('Email address') }}</Label>
                <Input
                    id="email"
                    type="email"
                    required
                    :tabindex="2"
                    autocomplete="email"
                    name="email"
                    placeholder="email@example.com"
                />
                <InputError :message="errors.email" />
            </div>

            <div class="grid gap-2">
                <Label for="password">{{ __('Password') }}</Label>
                <PasswordInput
                    id="password"
                    required
                    :tabindex="3"
                    autocomplete="new-password"
                    name="password"
                    :placeholder="__('Password')"
                    :passwordrules="passwordRules"
                />
                <InputError :message="errors.password" />
            </div>

            <div class="grid gap-2">
                <Label for="password_confirmation">{{
                    __('Confirm password')
                }}</Label>
                <PasswordInput
                    id="password_confirmation"
                    required
                    :tabindex="4"
                    autocomplete="new-password"
                    name="password_confirmation"
                    :placeholder="__('Confirm password')"
                    :passwordrules="passwordRules"
                />
                <InputError :message="errors.password_confirmation" />
            </div>

            <Button
                type="submit"
                class="mt-2 w-full"
                tabindex="5"
                :disabled="processing"
                data-test="register-user-button"
            >
                <Spinner v-if="processing" />
                {{ __('Create account') }}
            </Button>
        </div>

        <div class="text-center text-sm text-muted-foreground">
            {{ __('Already have an account?') }}
            <TextLink
                :href="login()"
                class="underline underline-offset-4"
                :tabindex="6"
                >{{ __('Log in') }}</TextLink
            >
        </div>
    </Form>
</template>
