<template>
    <!-- Bind this input field to data in this model using v-model. -->
    <!-- When this changes we are going to call the onChange method. -->
    <select @change="onChange()"
    v-model="selected" class="form-select mt-10 block w-full border p-3 rounded">
        <!-- Default option for selected. -->
        <option value="0">Select Country</option>

        <!-- Use v-for directive to loop through countries and create an option for each one. -->
        <option v-for="country in countries" :value="country.ID">
            <!-- We want to display the country name. -->
            {{country.Country}}
        </option>
    </select>
</template>

<script>
    export default {
        name: 'CountrySelect',
        props: ['countries'],
        data() {
            return {
                selected: 0
            }
        },
        methods: {
            onChange() {
                //Search for a country based on an ID.
                const country = this.countries.find((item) => item.ID == this.selected);

                //Pass an event upwards into the Home.vue file to change stats for country stats.
                //Need to send country data with the emit.
                this.$emit('get-country', country);
            }
        }
    }
</script>