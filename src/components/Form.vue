<template>
  <v-card class="mx-auto mt-5 mb-5" max-width="800">
    <v-form v-model="valid" ref="form" lazy-validation>
      <v-container>
          <!-- Personal information fields -->
        <p>Personal info</p>
        <v-row>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="firstname"
              :rules="nameRules"
              :counter="10"
              label="First name"
              required
              outlined
            ></v-text-field>
          </v-col>

          <v-col cols="12" md="6">
            <v-text-field
              v-model="lastname"
              :rules="nameRules"
              :counter="10"
              label="Last name"
              required
              outlined
            ></v-text-field>
          </v-col>

          <v-col cols="12" md="6">
            <v-text-field
              v-model="email"
              :rules= "emailRules"
              label="E-mail"
              outlined
            ></v-text-field>
          </v-col>

          <v-col cols="12" md="6">
            <v-text-field
              v-model="institution"
              label="Institution"
              required
              outlined
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <vue-tel-input-vuetify
              v-model="phone"
              :rules="numberRules"
              placeholder="Mobile number"
              required
              outlined
            ></vue-tel-input-vuetify>
          </v-col>
        </v-row>
        <!-- Address -->
        <p>Address <span class="red--text">*</span></p>
        <v-row>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="address1"
              :rules="addressRules"
              label="Address Line 1"
              :counter="30"
              required
              outlined
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="address2"
              label="Address Line 2 (optional)"
              required
              outlined
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="city"
              :rules="cityRules"
              label="City"
              required
              outlined
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="state"
              :rules="stateRules"
              label="State/ Province"
              required
              outlined
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="zipcode"
              :rules="zipcodeRules"
              type="number"
              :counter="10"
              label="Postal/ Zipcode"
              required
              outlined
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-autocomplete
              ref="country"
              v-model="country"
              :rules="[() => !!country || 'This field is required']"
              :items="countries"
              label="Country"
              placeholder="Select Country"
              required
              outlined
            ></v-autocomplete>
          </v-col>
        </v-row>
        <hr />
        <!-- Accompanying person fields -->
        <p class="mt-3">Accompanying Person Info</p>
        <v-row>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="firstnameA"
              :rules="nameRules"
              :counter="10"
              label="First name"
              required
              outlined
            ></v-text-field>
          </v-col>

          <v-col cols="12" md="6">
            <v-text-field
              v-model="lastnameA"
              :rules="nameRules"
              :counter="10"
              label="Last name"
              required
              outlined
            ></v-text-field>
          </v-col>

          <v-col cols="12" md="6">
            <v-text-field
              v-model="emailA"
              label="E-mail"
              :rules="emailRules"
              required
              outlined
            ></v-text-field>
          </v-col>

          <v-col cols="12" md="6">
            <v-text-field
              v-model="institutionA"
              label="Institution"
              required
              outlined
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <vue-tel-input-vuetify
              v-model="phoneA"
              required
              outlined
              :rules="numberRulesA"
            ></vue-tel-input-vuetify>
          </v-col>
        </v-row>
        <p>Address <span class="red--text">*</span></p>
        <v-row>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="address1A"
              :rules="addressRules"
              label="Address Line 1"
              :counter="30"
              required
              outlined
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="address2A"
              label="Address Line 2 (optional)"
              required
              outlined
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="cityA"
              :rules="cityRules"
              label="City"
              required
              outlined
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="stateA"
              :rules="stateRules"
              label="State/ Province"
              required
              outlined
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="zipcodeA"
              :rules="zipcodeRules"
              type="number"
              :counter="10"
              label="Postal/ Zipcode"
              required
              outlined
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-autocomplete
              ref="country"
              v-model="country"
              :rules="[() => !!country || 'This field is required']"
              :items="countries"
              label="Country"
              placeholder="Select Country"
              required
              outlined
            ></v-autocomplete>
          </v-col>
        </v-row>
        <v-row>
          <v-spacer></v-spacer>
          <v-btn
            type="submit"
            :disabled="!valid"
            color="primary"
            class="mr-5 mb-5"
            @click="validate"
            depressed
            rounded
            large
          >
            Submit
          </v-btn>
        </v-row>
      </v-container>
    </v-form>
  </v-card>
</template>

<script>
export default {
  data: () => ({
    valid: false,
    firstname: "",
    lastname: "",
    email: "",
    institution: "",
    phone:"",
    address1: "",
    address2: "",
    city: "",
    state: "",
    zipcode: "",
    country: "",

    firstnameA: "",
    lastnameA: "",
    emailA:"",
    institutionA:"",
    phoneA:"",
    address1A: "",
    address2A: "",
    cityA: "",
    stateA: "",
    zipcodeA: "",
    countryA: "",
    countries: [
      "Afghanistan",
      "Albania",
      "Algeria",
      "Andorra",
      "Angola",
      "Anguilla",
      "Antigua &amp; Barbuda",
      "Argentina",
      "Armenia",
      "Aruba",
      "Australia",
      "Austria",
      "Azerbaijan",
      "Bahamas",
      "Bahrain",
      "Bangladesh",
      "Barbados",
      "Belarus",
      "Belgium",
      "Belize",
      "Benin",
      "Bermuda",
      "Bhutan",
      "Bolivia",
      "Bosnia &amp; Herzegovina",
      "Botswana",
      "Brazil",
      "British Virgin Islands",
      "Brunei",
      "Bulgaria",
      "Burkina Faso",
      "Burundi",
      "Cambodia",
      "Cameroon",
      "Cape Verde",
      "Cayman Islands",
      "Chad",
      "Chile",
      "China",
      "Colombia",
      "Congo",
      "Cook Islands",
      "Costa Rica",
      "Cote D Ivoire",
      "Croatia",
      "Cruise Ship",
      "Cuba",
      "Cyprus",
      "Czech Republic",
      "Denmark",
      "Djibouti",
      "Dominica",
      "Dominican Republic",
      "Ecuador",
      "Egypt",
      "El Salvador",
      "Equatorial Guinea",
      "Estonia",
      "Ethiopia",
      "Falkland Islands",
      "Faroe Islands",
      "Fiji",
      "Finland",
      "France",
      "French Polynesia",
      "French West Indies",
      "Gabon",
      "Gambia",
      "Georgia",
      "Germany",
      "Ghana",
      "Gibraltar",
      "Greece",
      "Greenland",
      "Grenada",
      "Guam",
      "Guatemala",
      "Guernsey",
      "Guinea",
      "Guinea Bissau",
      "Guyana",
      "Haiti",
      "Honduras",
      "Hong Kong",
      "Hungary",
      "Iceland",
      "India",
      "Indonesia",
      "Iran",
      "Iraq",
      "Ireland",
      "Isle of Man",
      "Israel",
      "Italy",
      "Jamaica",
      "Japan",
      "Jersey",
      "Jordan",
      "Kazakhstan",
      "Kenya",
      "Kuwait",
      "Kyrgyz Republic",
      "Laos",
      "Latvia",
      "Lebanon",
      "Lesotho",
      "Liberia",
      "Libya",
      "Liechtenstein",
      "Lithuania",
      "Luxembourg",
      "Macau",
      "Macedonia",
      "Madagascar",
      "Malawi",
      "Malaysia",
      "Maldives",
      "Mali",
      "Malta",
      "Mauritania",
      "Mauritius",
      "Mexico",
      "Moldova",
      "Monaco",
      "Mongolia",
      "Montenegro",
      "Montserrat",
      "Morocco",
      "Mozambique",
      "Namibia",
      "Nepal",
      "Netherlands",
      "Netherlands Antilles",
      "New Caledonia",
      "New Zealand",
      "Nicaragua",
      "Niger",
      "Nigeria",
      "Norway",
      "Oman",
      "Pakistan",
      "Palestine",
      "Panama",
      "Papua New Guinea",
      "Paraguay",
      "Peru",
      "Philippines",
      "Poland",
      "Portugal",
      "Puerto Rico",
      "Qatar",
      "Reunion",
      "Romania",
      "Russia",
      "Rwanda",
      "Saint Pierre &amp; Miquelon",
      "Samoa",
      "San Marino",
      "Satellite",
      "Saudi Arabia",
      "Senegal",
      "Serbia",
      "Seychelles",
      "Sierra Leone",
      "Singapore",
      "Slovakia",
      "Slovenia",
      "South Africa",
      "South Korea",
      "Spain",
      "Sri Lanka",
      "St Kitts &amp; Nevis",
      "St Lucia",
      "St Vincent",
      "St. Lucia",
      "Sudan",
      "Suriname",
      "Swaziland",
      "Sweden",
      "Switzerland",
      "Syria",
      "Taiwan",
      "Tajikistan",
      "Tanzania",
      "Thailand",
      `Timor L'Este`,
      "Togo",
      "Tonga",
      "Trinidad &amp; Tobago",
      "Tunisia",
      "Turkey",
      "Turkmenistan",
      "Turks &amp; Caicos",
      "Uganda",
      "Ukraine",
      "United Arab Emirates",
      "United Kingdom",
      "United States",
      "Uruguay",
      "Uzbekistan",
      "Venezuela",
      "Vietnam",
      "Virgin Islands (US)",
      "Yemen",
      "Zambia",
      "Zimbabwe",
    ],
    // Rules to validate the form
    nameRules: [
      (v) => !!v || "Name is required",
      (v) => v.length <= 10 || "Field must be less than 10 characters",
    ],
    emailRules: [
              v => !!v || 'E-mail is required',
              v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
          ],
    addressRules: [
      (v) => !!v || "Address line 1 is required",
      (v) => v.length <= 30 || "Field must be less than 10 characters",
    ],
    numberRules: [
      (v) => !!v || "MobileNumber may not be empty",
      (v) => /^([+]\d{2})?\d{10}$/.test(v) || 'Number must be valid',
    ],
    numberRulesA: [
        (v) => !!v || "MobileNumber may not be empty",
      (v) => /^(\+\d{1,3}[- ]?)?\d{10}$/.test(v) || 'Number must be valid',
    ],
    cityRules: [
      (v) => !!v || "City is required",
      (v) => v.length <= 20 || "City must be less than 20 characters",
    ],
    stateRules: [
      (v) => !!v || "State is required",
      (v) => v.length <= 20 || "State must be less than 20 characters",
    ],
    zipcodeRules: [
      (v) => !!v || "This field may not be empty",
      (v) => v.length <= 10 || "Zipcode must be less than 10 number",
      (v) => v > 0 || "The value must be greater than zero",
    ],
  }),
  // Method to validate the form
  methods: {
      validate () {
        this.$refs.form.validate()
      },
  }
};
</script>
