<template>
    <div class="grow md:h-8 lg:h-14 xl:h-16 flex justify-center items-center rounded lg:rounded-lg shadow-sm bg-gray-50 hover:bg-gray-200 hover:cursor-pointer">
        <div class="text-gray-900 text-sm lg:text-xl">
            {{value}}
        </div>
    </div>
</template>

<script>
export default {
    props: {
        value: String
    }

}
</script>

<style>

</style>