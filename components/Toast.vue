<template>
    <div class="absolute -top-40 left-4 fixed inset-x-0 flex items-center justify-center h-screen">
        <div class="w-60 p-4 bg-gray-800 text-white rounded-lg shadow-lg">
            {{ message }}
        </div>
    </div>
</template>
  
<script>


export default {
    name: "ToastMessage",
    props: {
        isVisible: {
            type: Boolean,
            required: true,
        },
        message: {
            type: String,
            required: true,
        },
    },
    data() {
        return {

        }
    },



}
</script>