<template>
    <div>
        <header class="primary text-center white--text py-4">
            <h1 class="display-1 py-6">Cookie policy</h1>
        </header>
        <v-container class="mt-5 py-16">
            <v-row>
                <v-col cols="11" md="8" justify="center" class="offset-md-2">
                   
                </v-col>
            </v-row>
        </v-container>
    </div>
</template>
<script>
export default {
  head() {
    return {
      script: [
        { hid: 'CookieDeclaration', src: 'https://consent.cookiebot.com/a01a09ef-f0f0-45d4-b516-bd20342681d3/cd.js', async: true }
      ]
    }
  }
}
</script>
