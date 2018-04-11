<template>
  <div class="field-details">
    <h3>Field Details Section</h3>
    <div class="field-details-section">
      <div class="field-type-tags-section">
        <div class="selected-field-type">
          {{ selectedFieldType }}
          <h1>
            {{ selectedFieldType.name }}
          </h1>
          <div class="label-reference-section">
            <label name="display-label">
              Display Label
              <input
              type="text"
              class="display-label"
              name="display-label"
              v-model.lazy="fieldDetails.displayLabel"
              :placeholder="selectedFieldType.name"
              @blur="createReferenceName">
            </label>

            <label name="reference-name">
              Reference Name
              <input
              type="text"
              name="reference-name"
              v-model.lazy="fieldDetails.referenceName">
            </label>
          </div>

          <div class="value-validation-section">
            <label name="default-value">
              Default Value
              <input
              :type="selectedFieldType.inputType"
              name="default-value"
              v-model.lazy="fieldDetails.defaultValue">
            </label>

            <label name="custom-validation">
              Custom Validation
              <input
              type="text"
              name="custom-validation"
              v-model.lazy="fieldDetails.customValidation"
              @blur="checkIfRegEx">
            </label>
          </div>

        </div>
        <field-tags></field-tags>
      </div>
      <field-groups></field-groups>
    </div>
  </div>
</template>

<script>
// Imports
import FieldTypes from './FieldTypes.vue';
import FieldTags from './FieldTags.vue';
import FieldGroups from './FieldGroups.vue';

export default {
  props: {
    selectedFieldType: {
      type: Object,
      required: true
    }
  },
  components: {
    'field-types': FieldTypes,
    'field-tags': FieldTags,
    'field-groups': FieldGroups
  },
  data () {
    return {
      fieldDetails: {
        name: this.selectedFieldType.name,
        definition: this.selectedFieldType.definition,
        defaultDisplay: this.selectedFieldType.defaultDisplay,
        inputType: this.selectedFieldType.inputType,
        displayLabel: '',
        referenceName: '',
        defaultValue: '',
        customValidation: ''
      }
    //   blog: {
    //     title: '',
    //     content: '',
    //     categories: [],
    //     author: ''
    //   },
    //   authors: ['The Net Ninja', 'The Angular Avenger', 'The Vue Vindicator'],
    //   submitted: false
    }
  },
  methods: {
    createReferenceName: function() {
      console.log(this.fieldDetails.displayLabel);
      this.fieldDetails.referenceName = this.fieldDetails.displayLabel.replace(/\s+/g, '');
    },

    checkIfRegEx: function() {
      let regExString = this.fieldDetails.customValidation
      let regExInput = this.regExpFromString(regExString)
      console.log(regExInput);
      console.log (regExInput instanceof RegExp);
    },

    regExpFromString: function (q) {
      let flags = q.replace(/.*\/([gimuy]*)$/, '$1');
      if (flags === q) flags = '';
      let pattern = (flags ? q.replace(new RegExp('^/(.*?)/' + flags + '$'), '$1') : q);
      try { return new RegExp(pattern, flags); } catch (e) { return null; }
    }
  }
}
</script>

<style>
.field-details {
  flex-grow: 2;
}

.field-details-section {
  display: flex;
}
</style>
