<template>
  <div class="field-groups">
    <h4>Field groups</h4>
    <p>
      choose a group for this input
    </p>
    <div class="field-groups-section">
      <ul>
        <li
          v-for="fieldGroup in fieldGroups"
          @click="fieldGroup.groupIncreased = true"
          :class="{ 'active-tab': fieldGroup.groupIncreased }">
          {{ fieldGroup.fieldGroupName }}
          {{ fieldGroup.inputs.length }}
        </li>
      </ul>
      field groups go here

      <div class="add-group-button">
        add a new group
      </div>
    </div>
  </div>
</template>

<script>
// Imports
// import FieldTypes from './components/FieldTypes.vue';
// import FieldDetails from './components/FieldDetails.vue';

export default {
  components: {
    // 'field-types': FieldTypes,
    // 'field-details': FieldDetails
    // 'field-groups': FieldGroups,
    // 'field-tags': FieldTags
  },
  data () {
    return {
      fieldGroups: [
        {
          fieldGroupName: 'Rental Vehicle Coverage Package',
          groupIncreased: false,
          inputs: [
            {
              name: 'text',
              definition: 'String of Text',
              defaultDisplay: 'Free-form text input',
              inputType: 'text',
              displayLabel: 'Car Make',
              referenceName: 'carmake',
              defaultValue: 'Honda',
              customValidation: ''
            },
            {
              name: 'text',
              definition: 'String of Text',
              defaultDisplay: 'Free-form text input',
              inputType: 'text',
              displayLabel: 'Car Model',
              referenceName: 'carmodel',
              defaultValue: 'Civic',
              customValidation: ''
            },
            {
              name: 'Date',
              definition: 'Standard ISO format date',
              defaultDisplay: 'Datepicker, with configurable format',
              inputType: 'date',
              displayLabel: 'Rental Start Date',
              referenceName: 'RentalStartDate',
              defaultValue: '7/7/18',
              customValidation: ''
            },
            {
              name: 'Date',
              definition: 'Standard ISO format date',
              defaultDisplay: 'Datepicker, with configurable format',
              inputType: 'date',
              displayLabel: 'Rental End Date',
              referenceName: 'RentalEndDate',
              defaultValue: '7/10/18',
              customValidation: ''
            },
            {
              name: 'text',
              definition: 'String of Text',
              defaultDisplay: 'Free-form text input',
              inputType: 'text',
              displayLabel: 'Car License Number',
              referenceName: 'CarLicenseNumber',
              defaultValue: 'TIE8484',
              customValidation: ''
            },
            {
              name: 'text',
              definition: 'String of Text',
              defaultDisplay: 'Free-form text input',
              inputType: 'text',
              displayLabel: 'Car Type',
              referenceName: 'cartype',
              defaultValue: 'coupe',
              customValidation: ''
            },
            {
              name: 'VIN',
              definition: 'Vehicle Identification Number',
              defaultDisplay: 'Free-form text input',
              inputType: 'text',
              displayLabel: 'Car Vin',
              referenceName: 'carvin',
              defaultValue: '888888888888888',
              customValidation: ''
            }
          ]
        }
      ],
    }
  },
  methods: {
    onGroupClick: function(fieldGroup) {
      fieldGroup.groupIncreased = true;
    }
    // post: function(){
    //   this.$http.post('http://jsonplaceholder.typicode.com/posts', {
    //     title: this.blog.title,
    //     body: this.blog.content,
    //     userId: 1
    //   }).then(function(data){
    //     console.log(data);
    //     this.submitted = true;
    //   });
    // }
  }
}
</script>

<style>

</style>
