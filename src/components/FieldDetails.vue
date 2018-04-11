<template>
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
        @blur="createReferenceName"
        required />
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
      <div class="error" v-if="isInvalidRegex">
        Please insert valid Regexp
      </div>
    </div>
    <div class="form-errors" v-if="errors.length">
      <b>Please correct the following error(s):</b>
      <ul>
        <li v-for="error in errors">{{ error }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    selectedFieldType: {
      type: Object,
      required: true
    }
  },
  components: {
  },
  data () {
    return {
      fieldDetails: {
        displayLabel: '',
        referenceName: '',
        defaultValue: '',
        customValidation: '',
        fieldType: {}
      },
      isInvalidRegex: false,
      errors: []
    }
  },
  methods: {
    createReferenceName: function() {
      this.fieldDetails.referenceName = this.fieldDetails.displayLabel.replace(/\s+/g, '');
      this.checkForm();
    },

    checkIfRegEx: function() {
      let regExString = this.fieldDetails.customValidation
      let regExInput = this.regExpFromString(regExString)
      console.log(regExInput);
      console.log (regExInput instanceof RegExp);

      if (regExInput instanceof RegExp) {
        this.isInvalidRegex = false;
      } else {
        this.isInvalidRegex = true;
      }
    },

    regExpFromString: function (q) {
      let flags = q.replace(/.*\/([gimuy]*)$/, '$1');
      if (flags === q) flags = '';
      let pattern = (flags ? q.replace(new RegExp('^/(.*?)/' + flags + '$'), '$1') : q);
      try { return new RegExp(pattern, flags); } catch (e) { return null; }
    },

    sendFieldDetails: function() {
      this.$emit('fieldDetails', this.fieldDetails);
      this.checkForm();
    },

    resetFieldDetails: function() {
      this.fieldDetails.displayLabel = '';
      this.fieldDetails.referenceName = '';
      this.fieldDetails.defaultValue = '';
      this.fieldDetails.customValidation = '';
      this.fieldDetails.fieldType = {};
      this.isInvalidRegex = false;
    },

    checkForm:function() {
      if(this.fieldDetails.displayLabel && this.fieldDetails.referenceName) {
        this.errors = [];
      }
      if(!this.fieldDetails.displayLabel) this.errors.push("Display label required.");
      if(!this.fieldDetails.referenceName) this.errors.push("Reference name required.");
    }
  },
  created() {
    this.fieldDetails.fieldType = this.selectedFieldType;
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
