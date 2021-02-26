<template>
    <div id="theForm" class="theForm" light>
        <v-progress-linear v-model="percentageDone" height="10" color="orange accent-4"></v-progress-linear>
        <div v-for="(question, key, index) in questions" :key="key">
            <transition name="fade">
                <v-form v-on:submit.prevent v-model="isValid" v-if="key == 'id_like_quotes_for' && stepInner == index">
                    <div class="formSectionInner">
                        <h2 class="mb-5 text-center">I'd like quotes for...</h2>
                        <v-row>
                            <v-col>
                                <v-btn color="darkBlue" :outlined="questions[key] !=='myself'" :class="questions[key] =='myself' ? 'text-white' : null" height="80" x-large block @click="stepInner++, isSingle(), toTop()">
                                    <v-icon v-if="questions[key] =='myself'">mdi-radiobox-marked</v-icon>
                                    <v-icon v-else>mdi-radiobox-blank</v-icon>
                                    Just me
                                </v-btn>
                            </v-col>
                            <v-col>
                                <v-btn color="darkBlue" :outlined="questions[key] !=='myself_and_partner'" :class="questions[key] =='myself_and_partner' ? 'text-white' : null"  class="text-white text-left" height="80" x-large block @click="stepInner++, hasPartner(), toTop()">
                                    <v-icon v-if="questions[key] == 'myself_and_partner'">mdi-radiobox-marked</v-icon>
                                    <v-icon v-else>mdi-radiobox-blank</v-icon>
                                    Me & my partner
                                </v-btn>
                            </v-col>
                        </v-row>
                    </div>
                    <v-row class="trustLogos" align="center">
                        <v-col class="text-center mb-3 col">
                            <v-img class="ml-auto mr-auto" src="/reviews-trust-logo.png" width="65" /></v-col>
                        <v-col class="text-center mb-3 col">
                            <v-img class="ml-auto mr-auto" src="/comodo.png" width="65" /></v-col>
                        <v-col class="text-center mb-3 col">
                            <v-img class="ml-auto mr-auto" src="/ico.png" width="65" /></v-col>
                    </v-row>
                </v-form>
            </transition>
            <!-- smoker -->
            <transition name="fade">
                <v-form v-on:submit.prevent v-model="isValid" v-if="key == 'have_you_smoked_in_the_last_12_months' && stepInner == index">
                    <div class="formSectionInner">
                        <h2 class="mb-5 text-center">Have you smoked in the last 12 months?</h2>
                        <v-row>
                            <v-col>
                                <v-btn color="darkBlue" :outlined="questions[key] !=='yes'" :class="questions[key] =='yes' ? 'text-white' : null" height="80" x-large block @click="questions[key] = 'yes', stepInner++, toTop()">
                                    <v-icon v-if="questions[key] =='yes'">mdi-radiobox-marked</v-icon>
                                    <v-icon v-else>mdi-radiobox-blank</v-icon>
                                    Yes
                                </v-btn>
                            </v-col>
                            <v-col>
                                <v-btn color="darkBlue" :outlined="questions[key] !=='no'" :class="questions[key] =='no' ? 'text-white' : null" height="80" x-large block @click="questions[key] = 'no', stepInner++, toTop()">
                                    <v-icon v-if="questions[key] =='no'">mdi-radiobox-marked</v-icon>
                                    <v-icon v-else>mdi-radiobox-blank</v-icon>
                                    No
                                </v-btn>
                            </v-col>
                        </v-row>
                    </div>
                </v-form>
            </transition>
            <!-- partner smoker -->
            <transition name="fade">
                <v-form v-on:submit.prevent v-model="isValid" v-if="key == 'has_your_partner_smoked_in_the_last_12_months' && stepInner == index">
                    <div class="formSectionInner">
                        <h2 class="mb-5 text-center">Has your partner smoked in the last 12 months?</h2>
                        <v-row>
                           <v-col>
                                <v-btn color="darkBlue" :outlined="questions[key] !=='yes'" :class="questions[key] =='yes' ? 'text-white' : null" height="80" x-large block @click="stepInner++, questions[key] = 'yes', toTop()">
                                    <v-icon v-if="questions[key] =='yes'">mdi-radiobox-marked</v-icon>
                                    <v-icon v-else>mdi-radiobox-blank</v-icon>
                                    Yes
                                </v-btn>
                            </v-col>
                            <v-col>
                                <v-btn color="darkBlue" :outlined="questions[key] !=='no'" :class="questions[key] =='no' ? 'text-white' : null" height="80" x-large block @click="stepInner++, questions[key] = 'no', toTop()">
                                    <v-icon v-if="questions[key] =='no'">mdi-radiobox-marked</v-icon>
                                    <v-icon v-else>mdi-radiobox-blank</v-icon>
                                    No
                                </v-btn>
                            </v-col>
                        </v-row>
                    </div>
                </v-form>
            </transition>
            <!-- gender -->
            <transition name="fade">
                <v-form v-on:submit.prevent v-model="isValid" v-if="key == 'gender' && stepInner == index">
                    <div class="formSectionInner">
                        <h2 class="mb-5 text-center">Are you</h2>
                        <v-row>
                            <v-col>
                                <v-btn x-large block color="darkBlue" :outlined="questions[key] !=='male'" :class="questions[key] =='male' ? 'text-white' : null" height="80" @click="stepInner++, questions[key] = 'male', toTop()">
                                    <v-icon v-if="questions[key] =='male'">mdi-radiobox-marked</v-icon>
                                    <v-icon v-else>mdi-radiobox-blank</v-icon>
                                    Male
                                </v-btn>
                            </v-col>
                            <v-col>
                                <v-btn color="darkBlue" :outlined="questions[key] !=='female'" :class="questions[key] =='female' ? 'text-white' : null" height="80" x-large block @click="stepInner++, questions[key] = 'female', toTop()">
                                  <v-icon v-if="questions[key] =='female'">mdi-radiobox-marked</v-icon>
                                    <v-icon v-else>mdi-radiobox-blank</v-icon>
                                    Female
                                </v-btn>
                            </v-col>
                        </v-row>
                    </div>
                </v-form>
            </transition>
            <!-- partner gender -->
            <transition name="fade">
                <v-form v-on:submit.prevent v-model="isValid" v-if="key == 'partnersGender' && stepInner == index">
                    <div class="formSectionInner">
                        <h2 class="mb-5 text-center">What is you partners gender?</h2>
                        <v-row>
                            <v-col>
                                <v-btn x-large block color="darkBlue" :outlined="questions[key] !=='male'" :class="questions[key] =='male' ? 'text-white' : null" height="80" @click="stepInner++, questions[key] = 'male', toTop()">
                                    <v-icon v-if="questions[key] =='male'">mdi-radiobox-marked</v-icon>
                                    <v-icon v-else>mdi-radiobox-blank</v-icon>
                                    Male
                                </v-btn>
                            </v-col>
                            <v-col>
                                <v-btn color="darkBlue" :outlined="questions[key] !=='female'" :class="questions[key] =='female' ? 'text-white' : null" height="80" x-large block @click="stepInner++, questions[key] = 'female', toTop()">
                                  <v-icon v-if="questions[key] =='female'">mdi-radiobox-marked</v-icon>
                                    <v-icon v-else>mdi-radiobox-blank</v-icon>
                                    Female
                                </v-btn>
                            </v-col>
                        </v-row>
                    </div>
                </v-form>
            </transition>
            <!-- DOB -->
            <transition name="fade">
                <v-form v-on:submit.prevent v-if="key == 'dob' && stepInner == index" ref="form" v-model="isValid" :rules="ageCheck ? isValid = true : isValid = false">
                    <div class="formSectionInner">
                        <h2 class="mb-5 text-center">Date of birth</h2>
                        {{prePopDob}}
                        <v-row v-if="!$vuetify.breakpoint.xs">
                            <v-col>
                                <v-autocomplete label="Day" autofocus single-line v-model="questions[key][0]" :items="listDays"></v-autocomplete>
                            </v-col>
                            <v-col>
                                <v-autocomplete label="Month" single-line v-model="questions[key][1]" :items="listMonths"></v-autocomplete>
                            </v-col>
                            <v-col>
                                <v-autocomplete single-line label="Year" v-model="questions[key][2]" :items="listYears"></v-autocomplete>
                            </v-col>
                        </v-row>
                        <v-row v-else>
                            <v-col :cols="6" class="py-0">
                                <v-select class="pb-0 mb-0" label="Day" autofocus single-line v-model="questions[key][0]" :items="listDays"></v-select>
                            </v-col>
                            <v-col :cols="6" class="py-0">
                                <v-select class="pb-0 mb-0" label="Month" single-line v-model="questions[key][1]" :items="listMonths"></v-select>
                            </v-col>
                            <v-col cols="12" class="py-0">
                                <v-select label="Year" single-line v-model="questions[key][2]" :items="listYears"></v-select>
                            </v-col>
                        </v-row>
                        <div v-if="questions[key].length >= 3 && !ageCheck" class="py-2" style="color: red">Sorry. You must be between 50 to 75 to qualify</div>
                        <v-btn :disabled="!isValid" color="accent"  x-large block class="btn-ntx" @click="stepInner++, toTop()">Next <v-icon>mdi-menu-right-outline</v-icon> </v-btn>
                    </div>
                </v-form>
            </transition>
            <!-- Partner DOB -->
            <transition name="fade">
                <v-form v-on:submit.prevent v-if="key == 'partners_dob' && stepInner == index" ref="form" v-model="isValid">
                    <div class="formSectionInner">
                        <h2 class="mb-5 text-center">What is your partners date of birth</h2>
                        <v-row v-if="!$vuetify.breakpoint.xs">
                            <v-col>
                                <v-autocomplete label="Day" autofocus single-line v-model="questions[key][0]" :rules="[validationRules.required]" :items="listDays"></v-autocomplete>
                            </v-col>
                            <v-col>
                                <v-autocomplete label="Month" single-line v-model="questions[key][1]" :rules="[validationRules.required]" :items="listMonths"></v-autocomplete>
                            </v-col>
                            <v-col>
                                <v-autocomplete @click="defaultYear" single-line label="Year" v-model="questions[key][2]" :rules="[validationRules.required]" :items="listYears"></v-autocomplete>
                            </v-col>
                        </v-row>
                        <v-row v-else>
                            <v-col :cols="6" class="py-0">
                                <v-select class="pb-0 mb-0" label="Day" autofocus single-line v-model="questions[key][0]" :rules="[validationRules.required]" :items="listDays"></v-select>
                            </v-col>
                            <v-col :cols="6" class="py-0">
                                <v-select class="pb-0 mb-0" label="Month" single-line v-model="questions[key][1]" :rules="[validationRules.required]" :items="listMonths"></v-select>
                            </v-col>
                            <v-col cols="12" class="py-0">
                                <v-select label="Year" color="darkBlue" class="text-white" v-model="questions[key][2]" :rules="[validationRules.required]" :items="listYears"></v-select>
                            </v-col>
                        </v-row>
                        <v-btn :disabled="!isValid"  color="accent"  x-large block class="btn-ntx" @click="stepInner++, toTop()">Next <v-icon>mdi-menu-right-outline</v-icon></v-btn>
                    </div>
                </v-form>
            </transition>
            <!-- Name -->
            <transition name="fade">
                <v-form v-on:submit.prevent v-model="isValid" v-if="key == 'name' && stepInner == index">
                    <div class="formSectionInner formSectionInner--narrow">
                        <h2 class="mb-5 text-center">Your name</h2>
                        <v-radio-group v-model="questions[key][2]" row class="justify-space-between" :rules="[validationRules.required]">
                            <template v-for="(title, i ) in titles"><v-radio :label="title" :value="title" :key="i"></v-radio>
                            </template>
                        </v-radio-group>
                        <v-text-field single-line label="First name" :rules="[validationRules.required]" v-model="questions[key][0]"></v-text-field>
                        <v-text-field single-line label="Surname" :rules="[validationRules.required]" v-model="questions[key][1]"></v-text-field>
                        <v-btn :disabled="!isValid" color="accent" class="text-white btn-ntx" x-large block @click="stepInner++, toTop()">Next <v-icon>mdi-menu-right-outline</v-icon></v-btn>
                    </div>
                </v-form>
            </transition>
            <!-- Email -->
            <transition name="fade">
                <v-form v-on:submit.prevent v-if="key == 'email' && stepInner == index" ref="form" v-model="isValid">
                    <div class="formSectionInner formSectionInner--narrow">
                        <h2 class="mb-5 text-center">Email address</h2>
                        <v-text-field type="email" single-line label="Email" :rules="validationRules.email" v-model="questions[key]"></v-text-field>
                        <v-btn :disabled="!isValid"  x-large block color="accent" class="text-white btn-ntx" @click="stepInner++, toTop()">Next <v-icon>mdi-menu-right-outline</v-icon></v-btn>
                    </div>
                </v-form>
            </transition>
            <!-- Tel -->
            <transition name="fade">
                <v-form v-on:submit.prevent v-if="key == 'phone' && stepInner == index" ref="form" v-model="isValid" :intial="isValid = false">
                    <div class="formSectionInner formSectionInner--narrow telephone">
                        <h2 class="mb-5 text-center">Contact number</h2>
                        <v-text-field :hint="telSearching ? 'Verifying telephone number' : null"  ref="telephoneField" type="tel"  pattern="[0-9]*" single-line label="Telephone number" v-model="questions[key]" ></v-text-field>
                        <p v-if="phoneValidated == false">Invalid UK telephone number</p>
                        <v-btn height="80" :loading="telSearching || sending" color="accent" class="text-white btn-ntx mt-5" x-large block @click="phoneValidate(), toTop()">Get my Free Quote <v-icon>mdi-menu-right-outline</v-icon></v-btn>
                        <p class="mt-3"><small style="font-size:10px; line-height: 8px">By clicking <i>"Get my Free Quote"</i> you agree to be contacted by telephone or email by Promis Life, an FCA Authorised Firm, and confirm that you have read and agreed to our <a href="/terms-and-conditions.php" target="_blank">Terms & Conditions</a> and <a href="/privacy" target="_blank">Privacy Policy</a></small></p>
                    </div>
                </v-form>
            </transition>
            <!-- Address  -->
            <transition name="fade">
            <v-form v-on:submit.prevent transition="fade-transition" v-if="key == 'address' && stepInner == index"  :rule="questions[key].length !== 0 && questions[key].line_1 && questions[key].postcode && questions[key].post_town ? isValid = true: isValid = false" >
                <div class="formSectionInner">
                    <h2 class="mb-5 text-center">What is your address?</h2>
                    <v-row no-gutters>
                        <v-col cols="8">
                            <input type="text" v-model="searchPostcode" ref="postcodeField" class="addressLookup" :placeholder="!$vuetify.breakpoint.xs ? 'Please type your postcode' : 'Your postcode'" @change="requestAddress(key)">
                        </v-col>
                        <v-col cols="4" class="pl-1">
                            <v-btn @click="requestAddress(key)" color="accent" x-large block><v-icon v-show="!$vuetify.breakpoint.xs">mdi-home-search-outline</v-icon> Find</v-btn>
                        </v-col>
                    </v-row>
                    <br>
                    <v-dialog v-model="popUp" scrollable dark max-width="400px">
                        <v-card>
                            <v-card-title>Select address</v-card-title>
                            <v-divider></v-divider>
                            <v-card-text style="height: 300px;">
                                <v-list>
                                    <v-list-item-group v-model="questions[key]">
                                        <v-list-item v-for="(address, i) in addressList" :key="i" :value="address" @click="popUp = false">
                                            {{address.line_1}}
                                        </v-list-item>
                                    </v-list-item-group>
                                </v-list>
                            </v-card-text>
                            <v-divider></v-divider>
                        </v-card>
                    </v-dialog>
                    <template v-if="questions[key]">
                        <v-row class="addressDeets">
                            <v-col cols="12" class="pb-0">
                                <v-text-field type="text" v-model="questions[key].line_1" single-line label="Address line 1" />
                            </v-col>
                            <v-col cols="12" class="pb-0">
                                <v-text-field type="text" v-model="questions[key].line_2" single-line label="Address line 2" />
                            </v-col>
                            <v-col cols="12" class="pb-0">
                                <v-text-field type="text" v-model="questions[key].line_3" d single-line label="Address line 3" />
                            </v-col>
                            <v-col cols="6" class="pb-0">
                                <v-text-field type="text" v-model="questions[key].post_town" d single-line label="Town/city" />
                            </v-col>
                            <v-col cols="6" class="pb-0">
                                <v-text-field disabled type="text" v-model="questions[key].postcode" single-line label="Postcode" />
                            </v-col>
                        </v-row>
                    </template>
                    <v-btn :disabled="!isValid" color="accent" class="text-white btn-ntx" x-large block  @click="stepInner++, toTop()">Next <v-icon>mdi-menu-right-outline</v-icon></v-btn>
                </div>
            </v-form>
            </transition>
         
           

        </div>
        <v-btn :disabled="sending" v-if="stepInner !== 0" text @click="stepInner--, toTop()" block class="btnBck"><v-icon>mdi-menu-left-outline</v-icon>Back</v-btn>
    </div>
</template>
<script>
import Vue from 'vue';
export default {
    name: 'theForm',
    data() {
        return {
            questions: {
                id_like_quotes_for: '',
                have_you_smoked_in_the_last_12_months: '',
                dob: [],
                gender: '',
                address: [],
                name: [],
                email: '',
                phone: null,
                success: false,
            },
            userIP: '',
            searchTelephone: '',
            searchPostcode: '',
            telSearching: false,
            phoneValidated: null,
            contactTicked: true,
            popUp: false,
            titles: ['Mr', 'Mrs', 'Miss', 'Ms'],
            addressList: [],
            sCount: 0,
            stepInner: 0, // must start at 0
            current: 0,
            numberOfsections: 0,
            isValid: false,
            gotVal: 0,
            submitError: "",
            notEligable: false,
            sending: false,
            formSuccess: false,
            validationRules: {
                required: (value) => !!value || "Required.",
                counter: (value) => !!value.length <= 11 || "Min 11 numbers",
                email: [
                    (v) => !!v || "E-mail is required",
                    (v) => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(v) || "E-mail must be valid",
                ],
                telephoneRules: [
                    (v) => v != null && !!v || "Required",
                    (v) => v.match(/^[0-9]+$/) || "Not a valid number",
                    (v) => v != null && v.length > 10 || "Not a valid number",
                ],
            },
        }
    },
    methods: {
        defaultYear() {
            alert('year')
        },
        hasPartner() {
            this.questions.id_like_quotes_for = 'myself_and_partner'
            this.addItem('questions', 'has_your_partner_smoked_in_the_last_12_months', '', 2);
            this.addItem('questions', 'partners_dob', [], 4);
            this.addItem('questions', 'partnersGender', '', 6);
        },
        isSingle() {
            this.questions.id_like_quotes_for = 'myself'
            this.removeItem('has_your_partner_smoked_in_the_last_12_months')
            this.removeItem('partners_dob')
            this.removeItem('partnersGender')
        },
        removeItem(q) {
            // finds the index
            Vue.delete(this.questions, q);
        },
        addItem(s, k, v, o) {
            function toObject(pairs) {
                return Array.from(pairs).reduce(
                    (acc, [key, value]) => Object.assign(acc, { [key]: value }),
                    {},
                );
            }
            //section - key - value - order/index
            // make a new array
            const newArr = new Array();
            // push old values to the new array
            Object.entries(this[s]).forEach(([key, value]) => {
                newArr.push([key, value]);
            });
            // add new items to array
            newArr.splice(o, 0, [k, v]);
            this.questions = toObject(newArr)
        },
        requestAddress(qKey) {
            this.$axios.$get('https://api.ideal-postcodes.co.uk/v1/postcodes/' + this.searchPostcode.replace(/\s/g, '') + '?api_key=###########')
                .then((response) => {
                    // console.log(response.result);
                    this.popUp = true
                    this.addressList = response.result
                })
                .catch(function(error) {
                    console.log(error);
                });
        },
        toTop() {
            this.$vuetify.goTo(0)
        },
        phoneValidate() {
            this.telSearching = true
            this.$axios.$post('https://webservices.data-8.co.uk/TelephoneLineValidation/IsValidAdvanced.json?key=###########', {
                    "number": this.questions.phone,
                    "options": {
                        "UseMobileValidation": true
                    }
                })
                .then((response) => {
                    if (response.Result == 'Invalid' ) {
                        this.isValid = false
                        this.phoneValidated = false
                        this.telError = 'This is not a valid UK number'
                    } else {
                        this.postLead
                    }
                    this.telSearching = false
                })
                .catch((error) => {
                    this.isValid = false
                    this.telError = 'This is not a valid UK number'
                    setTimeout(() => {
                        this.telError = '';
                    }, 2000);
                    console.log(error);
                    this.telSearching = false
                });
        },
        encodeDataToURL(data) {
            return Object.keys(data).map(value => `${value}=${encodeURIComponent(data[value])}`).join('&');
        },
        postLead() {
            this.sending = true
            const data = {
                "campid": "FOREVERPROTECT",
                "campaign_id": '606',
                "supplier_id": '479',
                "email": this.questions.email,
                "nameTitle": this.questions.name[2],
                "firstname": this.questions.name[0],
                "lastname": this.questions.name[1],
                "building": this.questions.address.building_number,
                "street1": this.questions.address.line_1,
                "street2": this.questions.address.line_2,
                "street3": this.questions.address.line_3,
                "towncity": this.questions.address.post_town,
                "county": this.questions.address.county,
                "postcode": this.questions.address.postcode,
                "phone1": this.questions.phone.replace(/\D/g,''),
                "dob": this.questions.dob.join('/'),
                "consumer_ip_address": this.userIP
            }
            const URL = "https://forever-protect-over-50.com/sendData.php"
            console.log(this.encodeDataToURL(data).toString().replace(/[^\x20-\x7E]/g, ''))
            this.$axios.$post(URL + "?" + this.encodeDataToURL(data).toString().replace(/[^\x20-\x7E]/g, '')
            ).then((response) => {
                this.sending = false
                console.log(response.code);
                window.location.replace('/success')
            }).catch(function(error) {
                console.log(error);
            });
        }
    },
    computed: {
        telLength(){
            if(this.questions.phone !== null){
               return this.questions.phone.toString().length < 10 ? false : true
            }
        },
        isLocalHost() {
            return location.hostname === "localhost" ? true : false
        },
        prePopDob() {
            this.questions.dob = [] ? this.questions.dob = [1, 1, 1969] : null;
        },
        ageCheck() {
            var today_date = new Date();
            var today_year = today_date.getFullYear();
            var today_month = today_date.getMonth();
            var today_day = today_date.getDate();
            var age = today_year - this.questions.dob[2];
            if (today_month < (this.questions.dob[1] - 1)) {
                age--;
            }
            if (((this.questions.dob[1] - 1) == today_month) && (today_day < this.questions.dob[0])) {
                age--;
            }
            return age >= 50 && age <= 75 ? true : false;
        },
        percentageDone() {
            var countAllQuestions = Object.keys(this.questions).length;
            var countAllValues = [];
            Object.values(this.questions).filter((y) => y == "" || y == 0 || y == [] || y == null)
                .forEach((q) => {
                    countAllValues.push(q);
                });
            var x = countAllValues.length / countAllQuestions;
            var percenage = x * 100;
            return 100 - percenage + "%";
        },
        listMonths() {
            var number = 1;
            var months = []
            for (var i = 1; i <= 12; i++) {
                months.push(number++);
            }
            return months
        },
        listDays() {
            var number = 1;
            var days = []
            for (var i = 1; i <= 31; i++) {
                days.push(number++);
            }
            return days
        },
        listYears() {
            var currentYear = new Date().getFullYear() - 17
            var years = [];
            var startYear = 1920;
            for (var i = startYear; i <= currentYear; i++) {
                years.push(startYear++);
            }
            return years.reverse()
        },
        randNum() {
            if (this.gotVal === 0) {
                var rand = Math.floor(Math.random() * (980 - 880 + 1)) + 880
                this.gotVal = rand
                console.log('new number ')
                return rand
            } else {
                console.log('old number ')
                return this.gotVal
            }
        }
    },
    mounted() {
        // get user IP
        fetch('https://api.ipify.org?format=json')
            .then(x => x.json()).then(({ ip }) => {
                this.userIP = ip;
            });
    }
}
</script>
<style scoped lang="scss">
.darkBlue{
    color: #fff !important;
}
.btn-ntx {
    color: #fff;
    font-family: $heading-font-family !important;
}
.btnBck .v-icon {
    color: orange !important;
}
.formSectionInner .v-btn {
    font-family: $heading-font-family !important;
    font-size: 1em;
    font-weight: bolder;
}
.v-btn .v-icon {
    margin-right: 10px;
    //color: #fff;
}
.theForm {
    background-color: #fff;
    border-radius: 8px;
    box-shadow: 0 1px 7px 0 rgba(0, 0, 0, .1), 0 1px 2px 0 rgba(0, 0, 0, .37);
    max-width: 600px;
    overflow: hidden;
    @media screen and (max-width:400px) {
        margin: -25px auto 0 auto;
        width: 95%;
    }
    @media screen and (min-width:400px) and (max-width:600px) {
        margin: -70px auto 0 auto;
        width: 95%;
    }
    @media screen and (min-width:600px) and (max-width:960px) {
        margin: -100px auto 0 auto;
    }
    @media only screen and (min-width: 960px) {
        margin: -150px auto 0 auto;
    }
}
.fade-enter-active,
.v-stepper__content {
    transition: all .3s ease-in-out !important;
}
.v-stepper {
    box-shadow: none !important;
    box-shadow: 0 !important;
}
.fade-enter-active,
.fade-leave-active,
.v-stepper__content {
    opacity: 1;
    transform: translateY(0)
}
.fade-enter {
    transition-delay: 3s
}
.fade-enter,
.fade-leave-to {
    opacity: 0;
    transform: translateY(10px)
}
.formSectionInner {
    @media only screen and (max-width: 600px) {
        padding: 1em;
    }
    @media only screen and (min-width: 600px) {
        padding: 1em;
    }
}
.addressLookup {
    background-color: #fff;
    padding: 0.5rem 1rem;
    border-radius: 0.3125rem;
    -moz-appearance: textfield;
    background-color: #fff;
    border: 1px solid #ddd !important;
    border-radius: 8px;
    display: block;
    font-size: 1rem;
    line-height: 1.5;
    max-width: 100%;
    min-height: 1.5rem;
    min-width: 3rem;
    padding: 0.4375rem 0.875rem;
    transition: border-color 0.15s;
    width: 100%;
    padding: 13px 10px;
    box-shadow: 0 2px 3px #00000014;
}
.addressDeets {
    .v-text-field__details {
        display: none !important;
    }
}
.addressField-0 {
    width: 40%;
    display: inline-block;
}
.addressField-1 {
    width: 100%;
    display: inline-block;
}
.addressField-2 {
    width: 60%;
    display: inline-block;
    padding-right: 12px;
}
.addressField-3 {
    width: 40%;
    display: inline-block;
}
.text-white{
    color: #fff;
}
</style>
