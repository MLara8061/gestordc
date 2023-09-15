<template>
    <Head title="departments" />

    <AuthenticatedLayout>
        <template #header>
        Proveedores
        </template>

        <div class="py-12">
          <div class="bg-white grid v-screen place-items-center">
          <div class="mt-3 mb-3 flex">
            <a :href="route('departments.create')" class="px-4 py-2 bg-gray-800 text-white border rounded-md font-semibold text-xs">
                <i class="fa-solid fa-plus-circle"></i> Añadir
            </a>
       </div>
    </div>
    </div>
    <div class="bg-white grid v-screen place-items-center">
        <table class="table-auto border border-gray-400">
            <thead>
                <tr class="bg-gray-100">
                    <th class="px-4 py-4">#</th>
                    <th class="px-4 py-4">DEPARTAMENTO</th>
                    <th class="px-4 py-4"></th>
                    <th class="px-4 py-4"></th>

                </tr>
            </thead>
            <tbody>
                <tr v-for="dep, i in departments" :key="dep.id">
                <td class="border border-gray-400 px-4 py-4">{{ (i+1) }}</td>
                <td class="border border-gray-400 px-4 py-4">{{ dep.name }}</td>
                <td class="border border-gray-400 px-4 py-4">
                    <a :href="route('departments.edit', dep.id)" class="px-4 py-2 bg-yellow-400 text-white border rounded-md font-semibold text-xs">
                    <i class="fa-solid fa-edit"></i>
                </a>
                </td>
                <td class="border border-gray-400 px-4 py-4">
                    <DangerButton @click="$event => deleteDepartment(dep.id,dep.name)">
                     <i class="fa-solid fa-trash"></i>
                    </DangerButton>
                </td>
                </tr>
            </tbody>

        </table>
   </div>

    </AuthenticatedLayout>
</template>

<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue'
import { Head, Link, useForm } from '@inertiajs/vue3';
import DangerButton from '@/Components/DangerButton.vue';
import Swal from 'sweetalert2';
import { Result } from 'postcss';

const props = defineProps({
    departments: {type:Object}
});

const form = useForm({
    id:''
});

const deleteDepartment = (id, name) =>{
    const alerta = Swal.mixin({
        buttonsStyling:true
    });

    alerta.fire({
        title:'Seguro de eliminar '+name+ ' ?',
        icon:'question', showCancelButton:true,
        confirmButtonText:'<i class="fa-solid fa-check"></i> Si,eliminar',
        cancelButtonText:'<i class="fa-solid fa-ban"></i> Cancelar',
    }).then((result) => {
         if(result.isConfirmed){
            form.delete(route('departments.destroy', id));
         }
    });
}
</script>
