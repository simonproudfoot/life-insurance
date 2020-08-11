<template>
    <div>
        <header style="height: 320px" class="primary text-center white--text py-4">
            <h1 class="display-1 pt-6">Compare Over 50 Life Insurance Quotes</h1>
            <h3>Affordable premiums from just £1.15 per week*</h3>
        </header>
        <theForm/>
        <v-container class="py-16">
            <v-row>
                <v-col class="text-center" cols="12" sm="6" md="3">
                    <div class="px-3">
                        <h3><v-icon large>mdi-shield-check</v-icon></h3>
                        <p><b>Guaranteed acceptance</b>, with no medical for UK residents aged 50-79</p>
                    </div>
                </v-col>
                <v-col class="text-center" cols="12" sm="6" md="3">
                    <div class="px-3">
                        <h3><v-icon large>mdi-shield-check</v-icon></h3>
                        <p><b>Fixed monthly premium options</b> available</p>
                    </div>
                </v-col>

                <v-col class="text-center" cols="12" sm="6" md="3">
                    <div class="px-3">
                        <h3><v-icon large>mdi-shield-check</v-icon></h3>
                        <p>Cover amounts from <b>£1,000 to £20,000</b> depending on the provider</p>
                    </div>
                </v-col>

                <v-col class="text-center" cols="12" sm="6" md="3">
                    <div class="px-3">
                       <h3><v-icon large>mdi-shield-check</v-icon></h3>
                        <p>Stop paying Premiums at age 90, but <b>cover continues for life.</b></p>
                    </div>
                </v-col>
            </v-row>
        </v-container>
    </div>
</template>

<script>
import theForm from '~/components/theForm.vue'
export default {
    components: {
        theForm,
    },

}
</script>
