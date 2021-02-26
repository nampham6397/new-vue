<template>
    <v-container>
        <v-row>
            <v-col>
                <h1>Signup Page</h1>
                <v-form ref="signUpForm" v-model="formValidity">
                    <v-text-field label="Email" type="email" v-model="email" :rules="emailRules"></v-text-field>
                    <v-autocomplete label="What browser do you use?" :items="browsers"></v-autocomplete>
                    <v-file-input label="Attach profile picture"></v-file-input>
                    <v-col cols="12" sm="6" md="4">
                        <v-menu
                            v-model="menu2"
                            :close-on-content-click="false"
                            :nudge-right="40"
                            transition="scale-transition"
                            offset-y
                            min-width="auto">
                            <template v-slot:activator="{ on, attrs }">
                            <v-text-field
                                v-model="date"
                                label="Birthday"
                                prepend-icon="mdi-calendar"
                                readonly
                                v-bind="attrs"
                                v-on="on"
                            ></v-text-field>
                            </template>
                            <v-date-picker
                            v-model="date"
                            @input="menu2 = false"
                            ></v-date-picker>
                        </v-menu>
                        </v-col>
                        <v-switch label="Agree to terms & conditions"></v-switch>
                        <v-btn type="submit" color="primary" class="mr-4" :disabled="!formValidity">Submit</v-btn>
                        <v-btn color="warning" class="mr-4" @click="resetValidation">Reset Validation</v-btn>
                        <v-btn color="error" @click="resetForm">Reset</v-btn>
                </v-form>
            </v-col>
        </v-row>
    </v-container>
</template>
<script>
export default {
    data: () => ({
        browsers: ['Chrome', 'Firefox', 'Safari', 'Edge', 'Opera'],
        date: new Date().toISOString().substr(0, 10),
        menu: false,
        modal: false,
        menu2: false,
        email: '',
        emailRules: [
        value => value.indexOf('@') !== 0 || 'Email should have a username.',
        value => value.includes('@') || 'Email should include an @ symbol.',
        value =>
        value.indexOf('.') - value.indexOf('@') > 1 ||
        'Email should contain a valid domain.',
        value => value.includes('.') || 'Email should include a period symbol.',
        value =>
        value.indexOf('.') <= value.length - 3 ||
        'Email should contain a valid domain extension.'
    ]
    }),
    methods: {
        resetForm() {
            this.$refs.signUpForm.reset()
        },
        resetValidation() {
            this.$refs.signUpForm.resetValidation()
        },
        validateForm() {
            this.$refs.signUpForm.validate()
        }
    }
}
</script>