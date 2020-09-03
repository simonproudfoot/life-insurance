<template>
    <div>

        <header style="height: 320px" class="primary text-center white--text py-4">
            <v-container>
                <h1 class="display-1 pt-6 page-title">Compare Over 50 Life Insurance Quotes</h1>
                <h3>Affordable premiums from just £1.15 per week*</h3>
            </v-container>
        </header>
        <theForm/>
        <v-container class="py-16">
            <v-row>
                <v-col class="text-center" cols="12" sm="6" md="3">
                    <div class="px-3">
                        <h3>
                            <v-icon large>mdi-shield-check</v-icon>
                        </h3>
                        <p><b>Guaranteed acceptance</b>, with no medical for UK residents aged 50-79</p>
                    </div>
                </v-col>
                <v-col class="text-center" cols="12" sm="6" md="3">
                    <div class="px-3">
                        <h3>
                            <v-icon large>mdi-shield-check</v-icon>
                        </h3>
                        <p><b>Fixed monthly premium options</b> available</p>
                    </div>
                </v-col>
                <v-col class="text-center" cols="12" sm="6" md="3">
                    <div class="px-3">
                        <h3>
                            <v-icon large>mdi-shield-check</v-icon>
                        </h3>
                        <p>Cover amounts from <b>£1,000 to £20,000</b> depending on the provider</p>
                    </div>
                </v-col>
                <v-col class="text-center" cols="12" sm="6" md="3">
                    <div class="px-3">
                        <h3>
                            <v-icon class="" large>mdi-shield-check</v-icon>
                        </h3>
                        <p>Stop paying Premiums at age 90, but <b>cover continues for life</b></p>
                    </div>
                </v-col>
            </v-row>
            <v-btn v-scroll="onScroll" v-show="fab > 700 && $vuetify.breakpoint.xs" fab dark fixed bottom right color="primary" @click="toTop">
                <v-icon>
                    mdi-arrow-up
                </v-icon>
            </v-btn>
        </v-container>
    </div>
</template>

<script>
import theForm from '~/components/theForm.vue'
export default {
    data: () => ({
        fab: false
    }),
    components: {
        theForm,
    },
    methods: {
        onScroll(e) {
           
            const top = window.pageYOffset || e.target.scrollTop || 0
            this.fab = top
           
        },
        toTop() {
            this.$vuetify.goTo(0)
        }
    }

}
</script>

<style scopped>
.v-application{ overflow-x:hidden }
.v-icon {
    color: orange;
}

@media screen and (max-width:600px) {
    .page-title {
        font-size: 0.5em !important;
    }
}

@media screen and (max-width:600px) {
    .v-footer {
        line-height: 20px
    }
}
</style>
