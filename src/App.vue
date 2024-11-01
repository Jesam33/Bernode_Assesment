<template>
  <div class="py-3 pb-8 w-full">
    <SignUpTopper />
    <div class="sm:w-[75%] px-3 md:px-0 mt-4 lg:w-[27%] mx-auto">
      <span class="flex items-center space-x-2">
        <font-awesome-icon :icon="['fas', 'chevron-left']" />
        <p class="text-[18px] font-[600]">Back</p>
      </span>
      <div class="mt-10 w-full">
        <h1 class="text-[30px] text-[#181919] font-[700]">Let's get started</h1>
        <p class="mt-3 text-[#181919] font-[400]">
          Enter your information just as it appears on your premium health insurance card or pay stub.
        </p>
        <p class="mt-4 text-[#181919] font-[300]">*Required</p>
      </div>
      <form @submit.prevent="validate" class="mt-8 space-y-4">
        <FormItem label="First Name" ItemId="first_name" v-model="first_name" :ItemError="fnameError" />
        <FormItem label="Last Name" ItemId="last_name" v-model="last_name" :ItemError="lnameError" />
        <FormItem label="Email" ItemId="email" v-model="email" :ItemError="emailError" :ItemType="'email'" />
        <SelectFormItem label="Country" ItemId="country" v-model="country" :options="dropdownOptions" />
        <FormItem label="ZIP Code" ItemId="zip_code" v-model="zip_code" :ItemError="zipCodeError" />
        <SelectFormItem label="Sex assigned at birth" ItemId="sex" v-model="sex" :options="dropdownOptions2" />
        <FormItem label="Date Of Birth" ItemId="DOB" v-model="DOB" :ItemError="dobError" :ItemType="'date'" />

        <div class="flex gap-3 mt-4">
          <input class="rounded-[15px] border border-black outline-none h-[20px] w-[20px] px-3" type="checkbox" v-model="hasCode" />
          <p>I received a Teladoc Health code from my employer or insurance company.</p>
        </div>
        <div v-if="hasCode">
          <FormItem label="Teladoc Health Code" v-model="teladocCode" />
        </div>
        <div class="w-full">
          <button class="px-3 w-full text-white font-[600] text-[18px] bg-[#5b2f91] py-3 rounded-[12px]">Next</button>
        </div>
      </form>
    </div>
    <div class="flex w-[80%] border-t pt-6 mx-auto justify-center mt-[10%] text-[13px] gap-4 font-[600]">
      <p class="text-gray-600">© 2002-2024 Teladoc, Inc. All rights reserved.</p>
      <p class="text-[#5b2f91]">Terms of Service</p>
      <p class="text-[#5b2f91]">Notice of Privacy Practices</p>
      <p class="text-[#5b2f91]">Notice of Non-Discrimination and Language Assistance</p>
    </div>
  </div>
</template>

<script>
import FormItem from "./components/FormItem.vue";
import SignUpTopper from "./components/SignUpTopper.vue";
import SelectFormItem from "./components/SelectFormItem.vue";

export default {
  name: "App",
  components: {
    SignUpTopper,
    FormItem,
    SelectFormItem,
  },
  data() {
    return {
      first_name: "",
      last_name: "",
      email: "",
      country: "0",
      zip_code: "",
      sex: "0",
      DOB: "",
      hasCode: false,
      teladocCode: "",

      // Error messages
      fnameError: "",
      lnameError: "",
      emailError: "",
      zipCodeError: "",
      dobError: "",

      dropdownOptions: [
        { value: "0", label: "Please select" },
        { value: "1", label: "United States Of America" },
        { value: "2", label: "Denmark" },
        { value: "3", label: "Afghanistan" },
        { value: "4", label: "Canada" },
        { value: "5", label: "Albania" },
        { value: "6", label: "Algeria" },
        { value: "7", label: "American Samoa" },
        { value: "8", label: "Andorra" },
        { value: "9", label: "Angola" },
        { value: "10", label: "Anguilla" },
        { value: "11", label: "Antigua and Barbuda" },
        { value: "12", label: "Argentina" },
        { value: "13", label: "Armenia" },
        { value: "14", label: "Australia" },
        { value: "15", label: "Austria" },
        { value: "16", label: "Azerbaijan" },
        { value: "17", label: "Bahamas" },
        { value: "18", label: "Bahrain" },
        { value: "19", label: "Bangladesh" },
        { value: "20", label: "Barbados" },
        { value: "21", label: "Belarus" },
        { value: "22", label: "Belgium" },
        { value: "23", label: "Belize" },
        { value: "24", label: "Benin" },
        { value: "25", label: "Bhutan" },
        { value: "26", label: "Bolivia" },
        { value: "27", label: "Bosnia and Herzegovina" },
        { value: "28", label: "Botswana" },
        { value: "29", label: "Brazil" },
        { value: "30", label: "Brunei" },
        { value: "31", label: "Bulgaria" },
        { value: "32", label: "Burkina Faso" },
        { value: "33", label: "Burundi" },
        { value: "34", label: "Cabo Verde" },
        { value: "35", label: "Cambodia" },
        { value: "36", label: "Cameroon" },
        { value: "37", label: "Canada" },
        { value: "38", label: "Central African Republic" },
        { value: "39", label: "Chad" },
        { value: "40", label: "Chile" },
        { value: "41", label: "China" },
        { value: "42", label: "Colombia" },
        { value: "43", label: "Comoros" },
        { value: "44", label: "Congo" },
        { value: "45", label: "Congo, Democratic Republic of the" },
        { value: "46", label: "Costa Rica" },
        { value: "47", label: "Croatia" },
        { value: "48", label: "Cuba" },
        { value: "49", label: "Cyprus" },
        { value: "50", label: "Czech Republic" },
        { value: "51", label: "Denmark" },
        { value: "52", label: "Djibouti" },
        { value: "53", label: "Dominica" },
        { value: "54", label: "Dominican Republic" },
        { value: "55", label: "Ecuador" },
        { value: "56", label: "Egypt" },
        { value: "57", label: "El Salvador" },
        { value: "58", label: "Equatorial Guinea" },
        { value: "59", label: "Eritrea" },
        { value: "60", label: "Estonia" },
        { value: "61", label: "Eswatini" },
        { value: "62", label: "Ethiopia" },
        { value: "63", label: "Fiji" },
        { value: "64", label: "Finland" },
        { value: "65", label: "France" },
        { value: "66", label: "Gabon" },
        { value: "67", label: "Gambia" },
        { value: "68", label: "Georgia" },
        { value: "69", label: "Germany" },
        { value: "70", label: "Ghana" },
        { value: "71", label: "Greece" },
        { value: "72", label: "Grenada" },
        { value: "73", label: "Guatemala" },
        { value: "74", label: "Guinea" },
        { value: "75", label: "Guinea-Bissau" },
        { value: "76", label: "Guyana" },
        { value: "77", label: "Haiti" },
        { value: "78", label: "Honduras" },
        { value: "79", label: "Hungary" },
        { value: "80", label: "Iceland" },
        { value: "81", label: "India" },
        { value: "82", label: "Indonesia" },
        { value: "83", label: "Iran" },
        { value: "84", label: "Iraq" },
        { value: "85", label: "Ireland" },
        { value: "86", label: "Israel" },
        { value: "87", label: "Italy" },
        { value: "88", label: "Jamaica" },
        { value: "89", label: "Japan" },
        { value: "90", label: "Jordan" },
        { value: "91", label: "Kazakhstan" },
        { value: "92", label: "Kenya" },
        { value: "93", label: "Kiribati" },
        { value: "94", label: "Korea, North" },
        { value: "95", label: "Korea, South" },
        { value: "96", label: "Kuwait" },
        { value: "97", label: "Kyrgyzstan" },
        { value: "98", label: "Laos" },
        { value: "99", label: "Latvia" },
        { value: "100", label: "Lebanon" },
        { value: "101", label: "Lesotho" },
        { value: "102", label: "Liberia" },
        { value: "103", label: "Libya" },
        { value: "104", label: "Liechtenstein" },
        { value: "105", label: "Lithuania" },
        { value: "106", label: "Luxembourg" },
        { value: "107", label: "Madagascar" },
        { value: "108", label: "Malawi" },
        { value: "109", label: "Malaysia" },
        { value: "110", label: "Maldives" },
        { value: "111", label: "Mali" },
        { value: "112", label: "Malta" },
        { value: "113", label: "Marshall Islands" },
        { value: "114", label: "Mauritania" },
        { value: "115", label: "Mauritius" },
        { value: "116", label: "Mexico" },
        { value: "117", label: "Micronesia" },
        { value: "118", label: "Moldova" },
        { value: "119", label: "Monaco" },
        { value: "120", label: "Mongolia" },
        { value: "121", label: "Montenegro" },
        { value: "122", label: "Morocco" },
        { value: "123", label: "Mozambique" },
        { value: "124", label: "Myanmar" },
        { value: "125", label: "Namibia" },
        { value: "126", label: "Nauru" },
        { value: "127", label: "Nepal" },
        { value: "128", label: "Netherlands" },
        { value: "129", label: "New Zealand" },
        { value: "130", label: "Nicaragua" },
        { value: "131", label: "Niger" },
        { value: "132", label: "Nigeria" },
        { value: "133", label: "North Macedonia" },
        { value: "134", label: "Norway" },
        { value: "135", label: "Oman" },
        { value: "136", label: "Pakistan" },
        { value: "137", label: "Palau" },
        { value: "138", label: "Palestine" },
        { value: "139", label: "Panama" },
        { value: "140", label: "Papua New Guinea" },
        { value: "141", label: "Paraguay" },
        { value: "142", label: "Peru" }
        // ... other countries
      ],
      dropdownOptions2: [
        { value: "0", label: "Please select" },
        { value: "1", label: "Male" },
        { value: "2", label: "Female" },
        { value: "3", label: "Other" },
      ],
    };
  },
  methods: {
    isValidEmail(email) {
      const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return emailPattern.test(email);
    },
    validate() {
      // Reset error messages
      this.fnameError = this.lnameError = this.emailError = this.zipCodeError = this.dobError = "";

      // Validation checks
      if (!this.first_name) {
        this.fnameError = "First Name is required";
      }
      if (!this.last_name) {
        this.lnameError = "Last Name is required";
      }
      if (!this.isValidEmail(this.email)) {
        this.emailError = "Please enter a valid email address.";
      }
      if (this.country === "0") {
        this.zipCodeError = "ZIP Code is required and should be a number";
      }
      if (!this.zip_code || isNaN(this.zip_code)) {
        this.zipCodeError = "ZIP Code is required and should be a number";
      }
      if (this.sex === "0") {
        this.zipCodeError = "ZIP Code is required and should be a number";
      }
      if (!this.DOB) {
        this.dobError = "Date of Birth is required";
      }

      // Show success if all fields are valid
      if (!this.fnameError && !this.lnameError && !this.emailError && !this.zipCodeError && !this.dobError) {
        alert("Successful Registration, all fields are valid!");
      }
    },
  },
};
</script>

<style scoped>
/* Add any component-specific styles here */
</style>
