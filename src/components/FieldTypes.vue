<template>
  <div class="field-types">
    <h3>Field types section</h3>
    <div class="filter-field-types">
      <label>Filter Types</label>
      <input type="text" v-model="search" />
    </div>
    <div class="field-types-section">
      <ul>
        <li
          v-for="fieldType in filteredFieldTypes"
          @click="showFieldDetails(fieldType)"
          :class="{ 'active-type': selectedFieldType == fieldType }">
          <h3 class="field-type-title">{{ fieldType.name }}</h3>
          <div class="field-type-definition">
            <h5>Definition</h5>
            <p>{{ fieldType.definition }}</p>
          </div>
          <div class="field-type-default-display">
            <h5>Default Display</h5>
            <p>{{ fieldType.defaultDisplay }}</p>
          </div>
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
          inputType: 'select',
          options: ['option-1','option-2'],
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

<style lang="scss">
  @import '../assets/scss/_mixins';

  .field-types {
    @include default-padding;
    background-color: $field-types-background-color;
    border-right: 1px solid $main-border-color;
    flex-grow: 1;
    overflow-y: scroll;
  }

  .filter-field-types {
    margin-bottom: 1rem;

    label {
      margin-bottom: 5px;
    }

    input {
      margin-bottom: 5px;
    }
  }

  .field-types-section {
    li {
      @include round-accent-border;
      background-color: #ffffff;
      display: block;
      margin-bottom: 10px;
      padding: 5px;

      p {
        margin-bottom: 15px;
      }

      &.active-type {
        background-color: $selected-field-type-background-color;
        color: #ffffff;

        h5 {
          color: #ffffff;
        }
      }
    }

    h5 {
      @include small-accent-text;
      margin-bottom: 10px;
    }
  }
</style>
