<template>
    <v-card>
        <v-img
                :src="banner.url"
                height="200px"
        ></v-img>
    </v-card>
</template>

<script>
    export default {
        name: "banner",
        props: ['banner']
    }
</script>

<style scoped>

</style>
