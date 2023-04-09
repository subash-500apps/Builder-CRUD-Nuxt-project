<template>
    <div>
        <!--Edit builder prefill-->
        <table class="min-w-full divide-y divide-gray-300">
            <thead class="bg-gray-50">
                <tr>
                    <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">NAME</th>

                    <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                        Email
                    </th>
                    <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                        PhoneNmber
                    </th>
                    <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                        Logo
                    </th>

                </tr>
            </thead>
            <tbody class="divide-y divide-gray-200 bg-white">
                <tr v-for="(user, index) in builderData.data._rawValue" :key="index">
                    <td class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-6">
                        {{ user.name }}
                    </td>
                    <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                        {{ user.email }}
                    </td>
                    <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                        {{ user.phone_number }}
                    </td>
                    <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                        {{ user.logo }}
                    </td>
                    <!--Edit Action-->
                    <td class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-6">
                        <PencilSquareIcon class="h-5 w-5 mr-3"  @click="emit('builderPrefillData', user, index)"
                             aria-hidden="true"></PencilSquareIcon>
                             <!--Delete Action-->
                        <TrashIcon class="h-5 w-5 " aria-hidden="true"></TrashIcon>
                    </td>

                </tr>

            </tbody>
        </table>
    </div>
</template>

<script lang="ts" setup>
import { defineProps, defineEmits } from "vue";
import { XMarkIcon, TrashIcon, PencilSquareIcon, CheckIcon } from "@heroicons/vue/24/outline"

// Define props
const propsdata = defineProps({
    builderData: {
        type: Object,
        default: () => { },
    },
});
// Define emit events
const emit = defineEmits(['builderPrefillData'])
</script>