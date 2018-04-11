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
          @click="onGroupClick(fieldGroup)"
          :class="{ 'active-tab': fieldGroup.groupIncreased }">
          {{ fieldGroup.fieldGroupName }}
          {{ fieldGroup.inputs.length }}
        </li>
      </ul>
      field groups go here

      <div class="add-group-button">
        <p @click="showInput = !showInput">
          add a new group
        </p>

        <div v-if="showInput">
          <input
            type="text"
            v-model.lazy="newFieldGroupName"
            placeholder="New Field Group" />
          <button @click="addFieldGroup">Submit</button>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
// Imports

export default {
  components: {
  },
  data () {
    return {
      showInput: false,
      newFieldGroupName: '',
      fieldGroups: [
        {
          fieldGroupName: 'Rental Vehicle Coverage Package',
          groupIncreased: false,
          inputs: [
            {
              displayLabel: 'Car Make',
              referenceName: 'carmake',
              defaultValue: 'Honda',
              customValidation: '',
              fieldType: {
                name: 'text',
                definition: 'String of Text',
                defaultDisplay: 'Free-form text input',
                inputType: 'text',
              }
            },
            {
              displayLabel: 'Car Model',
              referenceName: 'carmodel',
              defaultValue: 'Civic',
              customValidation: '',
              fieldType: {
                name: 'text',
                definition: 'String of Text',
                defaultDisplay: 'Free-form text input',
                inputType: 'text',
              }
            },
            {
              displayLabel: 'Rental Start Date',
              referenceName: 'RentalStartDate',
              defaultValue: '7/7/18',
              customValidation: '',
              fieldType: {
                name: 'Date',
                definition: 'Standard ISO format date',
                defaultDisplay: 'Datepicker, with configurable format',
                inputType: 'date',
              }
            },
            {
              displayLabel: 'Rental End Date',
              referenceName: 'RentalEndDate',
              defaultValue: '7/10/18',
              customValidation: '',
              fieldType: {
                name: 'Date',
                definition: 'Standard ISO format date',
                defaultDisplay: 'Datepicker, with configurable format',
                inputType: 'date',
              }
            },
            {
              displayLabel: 'Car License Number',
              referenceName: 'CarLicenseNumber',
              defaultValue: 'TIE8484',
              customValidation: '',
              fieldType: {
                name: 'text',
                definition: 'String of Text',
                defaultDisplay: 'Free-form text input',
                inputType: 'text'
              }
            },
            {
              displayLabel: 'Car Type',
              referenceName: 'cartype',
              defaultValue: 'coupe',
              customValidation: '',
              fieldType: {
                name: 'text',
                definition: 'String of Text',
                defaultDisplay: 'Free-form text input',
                inputType: 'text'
              }
            },
            {
              displayLabel: 'Car Vin',
              referenceName: 'carvin',
              defaultValue: '888888888888888',
              customValidation: '',
              fieldType: {
                name: 'VIN',
                definition: 'Vehicle Identification Number',
                defaultDisplay: 'Free-form text input',
                inputType: 'text'
              }
            }
          ]
        }
      ],
    }
  },
  methods: {
    onGroupClick: function(fieldGroup) {
      this.$emit('selectedFieldGroup', fieldGroup);
      fieldGroup.groupIncreased = true;
    },

    addFieldGroup: function() {
      this.fieldGroups.push({
        fieldGroupName: this.newFieldGroupName,
        inputs: []
      });
      this.showInput = false;
      this.newFieldGroupName = '';
    },

    resetFieldGroups: function() {
      this.fieldGroups.showInput = false;
      this.fieldGroups.newFieldGroupName = '';
      this.fieldGroups.forEach(function (value) {
          value.groupIncreased = false;
      });
    }
  }
}
</script>

<style>

</style>
