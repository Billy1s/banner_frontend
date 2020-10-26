<template>

    <v-app id="inspire">
        <v-app-bar
                app
                shrink-on-scroll
        >


            <v-toolbar-title>Banners</v-toolbar-title>

            <v-spacer></v-spacer>

        </v-app-bar>

        <v-main>
            <v-container>
                <v-row>
                    <v-text-field
                            label="Campaign ID"
                            hide-details="auto"
                            :loading="loading"
                            v-model="campaignId"
                            class="pa-md-4"
                    ></v-text-field>

                    <v-btn block @click="searchCampaignId">
                        Search
                    </v-btn>
                </v-row>
                <v-row>
                    <v-col
                            v-for="banner in banners.data"
                            :key="banner.id"
                            cols="3"
                    >
                        <banner :banner="banner"></banner>

                    </v-col>
                </v-row>
            </v-container>
        </v-main>
    </v-app>

</template>

<script>
    import axios from 'axios'
    import Banner from "@/components/banner";

    export default {
        name: "PageMain",
        components: {Banner},
        data() {
            return {
                campaignId: '',
                loading: false,
                banners: {}
            }
        },
        methods: {
            searchCampaignId() {
                this.loading = true
                console.log(this.campaignId)
                axios
                    .get('http://localhost:5000/campaigns/'+ this.campaignId.toString())
                    .then(response => (
                            this.banners = response,
                            this.loading = false
                    ))
            }
        }
    }
</script>

<style scoped>

</style>
