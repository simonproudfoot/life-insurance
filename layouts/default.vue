<template>
    <v-app>
        <v-app-bar absolute elevation="0" app class="text-center navbar">
            <nuxt-link style="margin: auto; cursor: pointer"  tag="img" :src="'/logo.png'" to="/" width="100">
            </nuxt-link>
        </v-app-bar>
        <v-main>
            <nuxt />
        </v-main>
        <v-footer app absolute>
            <div class="container">
                <div class="row">
                    <div class="col-md-4 copy text-left">
                        <p><small>lifecoverquoter.co.uk © 2020. All Rights Reserved.</small></p>
                    </div>
                    <div class="col-md-8 copy-links text-right"><small><span>  <nuxt-link to="/privacy">Privacy</nuxt-link></span> | <span><nuxt-link to="/terms-and-conditions">Terms &amp; Conditions</nuxt-link></span> | <span><nuxt-link to="/copyright">Copyright Notices</nuxt-link></span></small></div>
                </div>
            </div>
            <div class="container text-center">
                <div class="row">
                    <div class="col-md-12">
                        <p><small>The Quoter Network is a trading style of Veriform ltd and is authorised and regulated by the FCA as a credit broker.</small></p>
                        <p><small>Subject to our terms and conditions The Quoter Network will process the information you provide us and may pass this on to our named partners for marketing purposes.</small></p>
                        <p><small>Veriform Ltd is a company registered in England &amp; Wales, registration number 07195400 and registered at 145/147 Hatfield Road, St. Albans, Hertfordshire, AL1 4JY, Authorised and regulated by the Financial Conduct Authority, firm
                            reference number 690199.</small></p>
                        <p><small>The Quoter Network is not an insurance company nor able to offer any advice into any financial services regulated products. Any terms and conditions may vary for all of our partners.</small></p>
                        <p><small>We do not charge a fee for this service, but we do receive a commission directly from our partners following successful introductions from this website. Any information we provide is for the purposes of illustrating the products promoted
                            on this site only and should not be read as financial advice.</small></p>
                    </div>
                </div>
            </div>
        </v-footer>
    </v-app>
</template>
<script>
export default {
    data() {
        return {

        }
    }
}
</script>
<style scopped>
.navbar{
  background-color: #0b3868 !important;
}
</style>
