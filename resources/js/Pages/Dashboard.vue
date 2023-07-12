<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">Dashboard</h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 text-gray-900">
                        Selamat Datang! <span class="text-blue-500">{{ $page.props.auth.user.name }}</span>

                    </div>
                    <div style="width: 250px; padding: 10px;">
                        <img src="./Profile/img/profile.png" alt="">
                    </div>
                </div>
            </div>
            
        </div>  
    </AuthenticatedLayout>
</template>
