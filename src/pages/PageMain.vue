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
                    <v-col v-if="error">
                        <v-card>
                            <v-card-title>{{errorBanner.message}}</v-card-title>
                            <v-card-subtitle>{{errorBanner.action}}</v-card-subtitle>
                            <v-card-text>Status: {{errorBanner.status}}</v-card-text>
                        </v-card>
                    </v-col>
                    <v-col
                            v-else
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
                banners: {},
                error: false,
                errorBanner: {}
            }
        },
        methods: {
            searchCampaignId() {
                this.error = false
                this.loading = true
                console.log(this.campaignId)
                axios
                    .get('https://n12rztq0gb.execute-api.eu-west-1.amazonaws.com/dev/campaigns/' + this.campaignId.toString())
                    .then(response => {
                        console.log(response)
                        this.banners = response
                        this.loading = false
                    }).catch((eer) => {
                    this.errorBanner = eer.response.data
                    this.error = true
                    this.loading = false
                })
            }
        }
    }
</script>

<style scoped>

</style>
