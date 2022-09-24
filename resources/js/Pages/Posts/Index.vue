<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, Link, useForm } from '@inertiajs/inertia-vue3';

defineProps({
    posts: Array
})
const form = useForm();
function destroy(id) {
    if (confirm("Are you sure you want to delete this post?")) {
        form.delete(route('posts.destroy', id));
    }
}
</script>
<template>
    <div>

        <Head title="Posts" />
        <AuthenticatedLayout>
            <template #header>
                <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                    All Posts
                </h2>
            </template>

            <div class="py-12">
                <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">

                    <div class="my-2 text-end">
                        <Link :href="route('posts.create')"
                            class="inline-block py-2 px-4 bg-blue-500 text-white rounded text-xl">
                        Add New Post
                        </Link>
                    </div>

                    <div class="overflow-x-auto relative shadow-md bg-white">
                        <table class="w-full text-md text-left text-gray-500 dark:text-gray-400 rounded-md">
                            <thead
                                class="text-sm border text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                                <tr>
                                    <th scope="col" class="border py-2 px-4">S/N</th>
                                    <th scope="col" class="border py-2 px-4">title</th>
                                    <th scope="col" class="border py-2 px-4">Body</th>
                                    <th scope="col" class="border py-2 px-4">Action</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="post in posts" key="post.index" class="hover:bg-gray-100/80">
                                    <td class="border py-2 px-4">{{ post.id }}</td>
                                    <td class="border py-2 px-4">{{ post.title }}</td>
                                    <td class="border py-2 px-4">{{ post.body }}</td>
                                    <td class="border py-2 px-4">
                                        <div class="flex gap-2">
                                            <Link :href="route('posts.edit',post.id)"
                                                class="inline-block bg-green-200 text-green-900 py-2 px-3 rounded">
                                                Edit
                                            </Link>

                                            <button @click="destroy(post.id)" tabIndex="-1" type="button"
                                                className="inline-block bg-red-200 text-red-900 py-2 px-3 rounded">
                                                Delete
                                            </button>
                                        </div>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </AuthenticatedLayout>

    </div>
</template>


<style lang="scss" scoped>

</style>