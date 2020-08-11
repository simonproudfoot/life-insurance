<template>
    <div class="theForm">
      <v-progress-linear v-model="percentageDone"  color="orange accent-4"></v-progress-linear>
        <div v-for="(question, key, index) in questions" :key="key">
            <transition name="fade">
                <v-form v-on:submit.prevent v-model="isValid" v-if="key == 'id_like_quotes_for' && stepInner == index">
                    <div class="formSectionInner">
                        <h2 class="mb-5 text-center">I'd like quotes for...</h2>
                        <v-row>
                            <v-col>
                                <v-btn outlined x-large block @click="stepInner++, isSingle()">
                                    <v-icon>mdi-human-male</v-icon>
                                    Just me
                                </v-btn>
                            </v-col>
                            <v-col>
                                <v-btn outlined x-large block @click="stepInner++, hasPartner()">
                                    <v-icon>mdi-human-male-female</v-icon>
                                    Me & my partner
                                </v-btn>
                            </v-col>
                        </v-row>
                    </div>
                    <v-row class="trustLogos" align="center">
                        <v-col class="text-center mb-3 col"><v-img class="ml-auto mr-auto" src="/reviews-trust-logo.png" width="65"/></v-col>
                        <v-col class="text-center mb-3 col"><v-img class="ml-auto mr-auto" src="/comodo.png" width="65"/></v-col>
                        <v-col class="text-center mb-3 col"><v-img class="ml-auto mr-auto" src="/ico.png" width="65"/></v-col>
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
                                <v-btn x-large block outlined @click="stepInner++, questions[key] = 'yes', toTop()">
                                    <v-icon>mdi-check-circle-outline</v-icon>
                                    <h2>Yes</h2>
                                </v-btn>
                            </v-col>
                            <v-col>
                                <v-btn outlined x-large block @click="stepInner++, questions[key] = 'no', toTop()">
                                    <v-icon>mdi-close-circle-outline</v-icon>
                                    <h2>No</h2>
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
                                <v-btn x-large block outlined @click="stepInner++, questions[key] = 'yes', toTop()">
                                    <v-icon>mdi-check-circle-outline</v-icon>
                                    <h2>Yes</h2>
                                </v-btn>
                            </v-col>
                            <v-col>
                                <v-btn outlined x-large block @click="stepInner++, questions[key] = 'no', toTop()">
                                    <v-icon>mdi-close-circle-outline</v-icon>
                                    <h2>No</h2>
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
                                <v-btn x-large block outlined @click="stepInner++, questions[key] = 'male', toTop()">
                                    <v-icon>mdi-human-male</v-icon>
                                    <h2>Male</h2>
                                </v-btn>
                            </v-col>
                            <v-col>
                                <v-btn outlined x-large block @click="stepInner++, questions[key] = 'female', toTop()">
                                    <v-icon>mdi-human-female</v-icon>
                                    <h2>Female</h2>
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
                                <v-btn x-large block outlined @click="stepInner++, questions[key] = 'male', toTop()">
                                    <v-icon>mdi-human-male</v-icon>
                                    <h2>Male</h2>
                                </v-btn>
                            </v-col>
                            <v-col>
                                <v-btn outlined x-large block @click="stepInner++, questions[key] = 'female', toTop()">
                                    <v-icon>mdi-human-female</v-icon>
                                    <h2>Female</h2>
                                </v-btn>
                            </v-col>
                        </v-row>
                    </div>
                </v-form>
            </transition>
            <!-- DOB -->
            <transition name="fade">
                <v-form v-on:submit.prevent v-if="key == 'dob' && stepInner == index" ref="form" v-model="isValid">
                    <div class="formSectionInner">
                        <h2 class="mb-5 text-center">Date of birth</h2>
                        <v-row v-if="!$vuetify.breakpoint.xs">
                            <v-col>
                                <v-autocomplete label="Day" autofocus single-line v-model="questions[key][0]" :rules="[validationRules.required]" :items="listDays"></v-autocomplete>
                            </v-col>
                            <v-col>
                                <v-autocomplete label="Month" single-line v-model="questions[key][1]" :rules="[validationRules.required]" :items="listMonths"></v-autocomplete>
                            </v-col>
                            <v-col>
                                <v-autocomplete single-line label="Year" v-model="questions[key][2]" :rules="[validationRules.required]" :items="listYears"></v-autocomplete>
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
                                <v-select label="Year" single-line v-model="questions[key][2]" :rules="[validationRules.required]" :items="listYears"></v-select>
                            </v-col>
                        </v-row>
                        <v-btn :disabled="!isValid" x-large block class="btn-ntx" @click="stepInner++, toTop()">Next</v-btn>
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
                                <v-autocomplete single-line label="Year" v-model="questions[key][2]" :rules="[validationRules.required]" :items="listYears"></v-autocomplete>
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
                                <v-select label="Year" outlined v-model="questions[key][2]" :rules="[validationRules.required]" :items="listYears"></v-select>
                            </v-col>
                        </v-row>
                        <v-btn :disabled="!isValid" x-large block class="btn-ntx" @click="stepInner++, toTop()">Next</v-btn>
                    </div>
                </v-form>
            </transition>
            <!-- Name -->
            <transition name="fade">
                <v-form v-on:submit.prevent v-model="isValid" v-if="key == 'name' && stepInner == index">
                    <div class="formSectionInner formSectionInner--narrow  ">
                        <h2 class="mb-5 text-center">Your name</h2>
                        <v-radio-group v-model="questions[key][2]" row class="justify-space-between" :rules="[validationRules.required]">
                            <template v-for="(title, i ) in titles"><v-radio :label="title" :value="title" :key="i"></v-radio>
                        </template>
                        </v-radio-group>
                        <v-text-field   single-line label="First name" :rules="[validationRules.required]" v-model="questions[key][0]"></v-text-field>
                        <v-text-field  single-line label="Surname" :rules="[validationRules.required]" v-model="questions[key][1]"></v-text-field>
                         <v-btn :disabled="!isValid" x-large block class="btn-ntx" @click="stepInner++, toTop()">Next</v-btn>
                    </div>
                </v-form>
            </transition>
          <!-- Email -->
            <transition name="fade">
                <v-form v-on:submit.prevent v-if="key == 'email' && stepInner == index" ref="form" v-model="isValid">
                    <div class="formSectionInner formSectionInner--narrow">
                        <h2 class="mb-5 text-center">Email address</h2>
                        <v-text-field type="email"   single-line label="Email" :rules="validationRules.email" v-model="questions[key]"></v-text-field>
                         <v-btn :disabled="!isValid" x-large block class="btn-ntx" @click="stepInner++, toTop()">Next</v-btn>
                    </div>
                </v-form>
            </transition>
            <!-- Tel -->
            <transition name="fade">
                <v-form v-on:submit.prevent v-if="key == 'phone' && stepInner == index" ref="form" v-model="isValid" :rules="phoneValidated ? isValid = true : isValid=true">
                    <div class="formSectionInner formSectionInner--narrow telephone">
                        <h2 class="mb-5 text-center">Contact number</h2>
                        <v-text-field  :hint="telSearching ? 'Verifying telephone number' : null" :append-icon="telSearching ? 'mdi-loading' : 'mdi-loadingf'"  ref="telephoneField" type="tel"  single-line label="Telephone number" v-model="questions[key]" @keyup="phoneValidate"></v-text-field>
                        <p v-if="phoneValidated == false">Invalid UK telephone number</p>
                        <v-btn :disabled="!isValid" x-large block class="btn-ntx" @click="stepInner++, toTop()">Next</v-btn>
                    </div>
                </v-form>
            </transition>
            <!-- Address  -->
            <transition name="fade">
            <v-form v-on:submit.prevent transition="fade-transition" v-if="key == 'address' && stepInner == index"  :rule="questions[key].length !== 0 ? isValid = true: isValid = false" >
                <div class="formSectionInner">
                    <h2 class="mb-5 text-center">What is your address?</h2>
                    <v-row>
                        <v-col cols="8">
                            <input type="text" v-model="searchPostcode" ref="postcodeField" class="addressLookup" placeholder="Please type your postcode" @change="requestAddress(key)">
                        {{searchPostcode.replace(/\s/g,'')}}
                        </v-col>
                        <v-col cols="4">
                            <v-btn @click="requestAddress(key)" color="primary" x-large block>Find</v-btn>
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
                                <v-text-field type="text" v-model="questions[key].postcode" single-line label="Postcode" />
                            </v-col>
                        </v-row>
                    </template>
                    <v-btn :disabled="!isValid" x-large block class="btn-ntx" @click="stepInner++, toTop()">Next</v-btn>
                </div>
            </v-form>
            </transition>
            <transition name="fade">
            <div v-if="key == 'success' && stepInner == index" class="formSectionInner formSectionInner--narrow">
                <v-alert v-if="submitError" type="error">
                    <span class="">Error submitting form</span>
                    <ul v-for="(error, i) in submitError" :key="i">
                        <li>{{error}}</li>
                    </ul>
                </v-alert>
                <v-btn large accent class="submitButton py-3" x-large color="success" @click="postForm" :loading="sending" >
                  Get my Free Quote
                  <v-icon class="mb-0" large>mdi-chevron-double-right</v-icon>
                </v-btn>
                <p>We would like to use email, text and display notifications to let you know about <b>lifecoverquoter.co.uk</b> products and services. If you do not want to receive these, un-tick this box.
                <v-checkbox outlined v-model="contactTicked" class="d-inline selectItems" style="width: 10px; margin-left:10px; vertical-align: sub;"></v-checkbox>
                </p>
            </div>
        </transition>
        </div>
        <v-btn v-if="stepInner !== 0" text @click="stepInner--, toTop()" block=""><v-icon>mdi-menu-left-outline</v-icon>Back</v-btn>
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
                have_you_smoked_in_the_last_12_months: '', // or "have_you_invested_in_a_sipp" if false
                dob: [],
                gender: '',
                address: [],
                name: [],
                email: '',
                phone: null,
                success: false,
            },
            searchPostcode: '',
            contactTicked: true,
            popUp: false,
            titles: ['Mr', 'Mrs', 'Miss', 'Ms'],
            addressList: [],
            sCount: 0,
            stepInner: 4, // must start at 0
            section: 1, // must start at 1
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
                    (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
                ],
                telephoneRules: [
                    (v) => !!v || "Required",
                    (v) => v.match(/^[0-9]+$/) || "Not a valid number",
                    (v) => v.length > 10 || "Not a valid number",
                ],
            },
        }
    },
    methods: {
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
            //section - key - value - order/index
            // make a new array
            const newArr = new Array();
            // push old values to the new array
            Object.entries(this[s]).forEach(([key, value]) => {
                newArr.push([key, value]);
            });
            // add new items to array
            newArr.splice(o, 0, [k, v]);
            this.questions = Object.fromEntries(newArr)
        },
        requestAddress(qKey) {
            this.$axios.$post('https://api.ideal-postcodes.co.uk/v1/postcodes/' + this.searchPostcode.replace(/\s/g,'') + '?api_key=ak_jr1wo74l0sgSldKnJeTPAEo5QpHxw')
                .then((response) => {
                    console.log(response.data.result);
                    this.popUp = true
                    this.addressList = response.data.result
                })
                .catch(function(error) {
                    console.log(error);
                });
        },
        toTop () {
          this.$vuetify.goTo(0)
        },
        phoneValidate() {
            if (this.$refs.telephoneField[0]['value'].length > 10) {
                this.telSearching = true
                this.axios.post('https://webservices.data-8.co.uk/TelephoneLineValidation/IsValidAdvanced.json?key=CX3N-IDXM-XEFB-73WE', {
                        "number": this.$refs.telephoneField[0]['value'],
                        "options": {
                            "UseMobileValidation": true
                        }
                    })
                    .then((response) => {
                        console.log(response.data.Result);
                        response.data.Result == 'Invalid' || response.data.Result == 'TemporaryInvalid' ? this.phoneValidated = false : this.phoneValidated = true
                        this.telSearching = false
                    })
                    .catch((error) => {
                        this.telError = 'This is not a valid UK number'
                        setTimeout(() => {
                            this.telError = '';
                        }, 2000);
                        console.log(error);
                        this.telSearching = false
                    });
            }
        },

    },
    computed: {

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
}
</script>
<style scoped lang="scss">
.btn-ntx {
    color: #fff;
    font-family: $heading-font-family;
    background-color: #ffa000 !important;
}
.v-btn .v-icon {
    margin-right: 10px;
    color: #1976d2;
}
.theForm {
    background-color: #fff;
    border-radius: 8px;
    box-shadow: 0 1px 7px 0 rgba(0, 0, 0, .1), 0 1px 2px 0 rgba(0, 0, 0, .37);
    max-width: 600px;
    @media only screen and (max-width: 600px) {
        margin: -40px auto 0 auto;
        width: 95%;
    }
    @media only screen and (min-width: 600px) {
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
    padding: 2em;
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
</style>
