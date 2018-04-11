<template>
  <div class="field-types">
    <h3>Field types section</h3>
    <div class="filter-field-types">
      <p>
        Filter Types
      </p>
      <input type="text" v-model="search" placeholder="Date" />
    </div>
    <div class="field-types-section">
      field type options go here
      <ul>
        <li
        v-for="fieldType in filteredFieldTypes"
        @click="showFieldDetails(fieldType)"
        :class="{ 'active-tab': selectedFieldType == fieldType }">
        {{ fieldType.name }}
      </li>
      </ul>
    </div>
  </div>
</template>

<script>
// Imports

export default {
  props: {
    // fieldTypes: {
    //   type: Array,
    //   required: true
    // },
    selectedFieldType: {
      type: Object
    }
  },
  components: {
  },
  data () {
    return {
      search: '',
      fieldTypes: [
        {
          name: 'Text',
          definition: 'String of Text',
          defaultDisplay: 'Free-form text input',
          inputType: 'text'
        },
        {
          name: 'Date',
          definition: 'Standard ISO format date',
          defaultDisplay: 'Datepicker, with configureable format',
          inputType: 'date'
        },
        {
          name: 'VIN',
          definition: 'Vehicle Identification Number',
          defaultDisplay: 'Free-form text input',
          inputType: 'text'
        },
        {
          name: 'Currency',
          definition: 'Currency',
          defaultDisplay: 'Free-form text input',
          inputType: 'text'
         },
        {
          name: 'Select',
          definition: 'Select box',
          defaultDisplay: 'multiple preset options with a single choice',
          inputType: 'select'
        },
        {
          name: 'Number',
          definition: 'String with numbers',
          defaultDisplay: 'Free-form text input',
          inputType: 'number'
        }
      ]
    }
  },
  methods: {
    showFieldDetails: function (fieldType) {
      this.$emit('selectedFieldType', fieldType);
    },

    showFirstFieldType: function() {
      this.fieldTypes;
      this.$emit('selectedFieldType', this.fieldTypes[0]);
    }
  },
  created() {
    this.showFirstFieldType();
  },
  computed: {
    filteredFieldTypes: function() {
      return this.fieldTypes.filter((fieldType) => {
        let fieldTypeLowerCase = fieldType.name.toLowerCase()
        return fieldTypeLowerCase.match(this.search.toLowerCase());
      });
    }
  }
}
</script>

<style>
.field-types {
  flex-grow: 1;
  margin-right: 1em;
}

.active-tab {
  color: cornflowerblue;
  text-transform: uppercase;
}
</style>
