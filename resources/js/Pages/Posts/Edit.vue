<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, Link, useForm } from '@inertiajs/inertia-vue3';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import TextArea from '@/Components/TextArea.vue';
const props = defineProps({
    post:Object
})
const form = useForm({
    'title': props.post.title,
    'body': props.post.body
})
const submit = () => {
    form.put(route('posts.update', props.post.id));
}
</script>
<template>
    <div>

        <Head title="Posts" />
        <AuthenticatedLayout>
            <template #header>
                <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                    Create Edit
                </h2>
            </template>
            <div class="py-12">
                <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                    <div class="bg-white overflow-hidden p-4">
                        <div class="my-2 text-end">
                            <Link :href="route('posts.index')"
                                class="inline-block py-2 px-4  bg-rose-500 text-white rounded text-xl">
                            Back to list
                            </Link>
                        </div>
                        <div class="overflow-x-auto relative">
                            <form name="CreateForm" @submit.prevent="submit">
                                <div class="mb-3">
                                    <InputLabel for="title" value="Title" />
                                    <TextInput id="title" type="text" class="mt-1 block w-full" v-model="form.title"
                                         autofocus autocomplete="title" />
                                    <InputError class="mt-2" :message="form.errors.title" />
                                </div>
                                <div class="mb-3">
                                    <InputLabel for="body" value="Description" />
                                    <TextArea id="body" type="text" class="mt-1 block w-full" v-model="form.body"
                                         autofocus autocomplete="body" />
                                    <InputError class="mt-2" :message="form.errors.body" />
                                </div>
                                <PrimaryButton class="my-3" :class="{ 'opacity-25': form.processing }"
                                    :disabled="form.processing">
                                    Update
                                </PrimaryButton>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </AuthenticatedLayout>
    </div>
</template>



<style lang="scss" scoped>

</style>