<template>
  <div class="selected-field-type">
    <h1>
      {{ selectedFieldType.name }}
    </h1>
    <div class="label-reference-section">
      <div class="display-label">
        <label name="display-label">Display Label</label>
        <input
        type="text"
        class="display-label"
        name="display-label"
        v-model.lazy="fieldDetails.displayLabel"
        :placeholder="selectedFieldType.name"
        @blur="createReferenceName"
        required />
        <p class="small-accent-text">
          For display purposes, spaces allowed
        </p>
      </div>

      <div class="reference-name">
        <label name="reference-name">Reference Name</label>
        <input
        type="text"
        name="reference-name"
        v-model.lazy="fieldDetails.referenceName" />
        <p class="small-accent-text">
          Used to reference in calculations,
          no spaces allowed.
        </p>
      </div>
    </div>

    <div class="value-validation-section">
      <div
        v-if="selectedFieldType.inputType == 'select'"
        class="select-option-value">
        <select v-model="fieldDetails.defaultValue">
          <option
            v-for="option in selectedFieldType.options">
            {{ option }}
          </option>
        </select>
      </div>
      <div class="input-default-value" v-else>
        <label name="default-value">Default Value</label>
        <input
          :type="selectedFieldType.inputType"
          name="default-value"
          v-model.lazy="fieldDetails.defaultValue" />
      </div>

      <label name="custom-validation">Custom Validation</label>
      <input
        type="text"
        name="custom-validation"
        v-model.lazy="fieldDetails.customValidation"
        @blur="checkIfRegEx" />
        <p class="small-accent-text">
          Any regex can be used for custom input validation
        </p>
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

<style lang="scss">
  @import '../assets/scss/_mixins';
  
  .field-details {
    flex-grow: 2;
    padding: 1.2em 1em;
    overflow-y: scroll;
  }

  .label-reference-section {
    display: flex;
  }

  .field-details-section {
    display: flex;
  }
</style>
