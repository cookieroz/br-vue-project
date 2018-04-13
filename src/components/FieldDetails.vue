<template>
  <div class="selected-field-type">
    <div class="column">
      <div class="display-label">
        <label name="display-label">Display Label</label>
        <input
        type="text"
        class="display-label"
        name="display-label"
        v-model.lazy="fieldDetails.displayLabel"
        @blur="createReferenceName"
        required />
        <p class="small-accent-text">
          For display purposes, spaces allowed
        </p>
        <div class="error" v-if="hasNoDisplayLabel">
          Please insert a display label
        </div>
      </div>

      <div class="select-option-value"
        v-if="selectedFieldType.inputType == 'select'">
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

      <div class="custom-validation-section">
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
    </div>

    <div class="column">
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
      hasNoDisplayLabel: false
    }
  },
  methods: {
    createReferenceName: function() {
      if (this.fieldDetails.displayLabel) {
        this.fieldDetails.referenceName = this.fieldDetails.displayLabel.replace(/\s+/g, '');
        this.hasNoDisplayLabel = false;
      } else {
        this.hasNoDisplayLabel = true;
      }
    },

    checkIfRegEx: function() {
      let regExString = this.fieldDetails.customValidation
      let regExInput = this.regExpFromString(regExString)

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
    },

    resetFieldDetails: function() {
      this.fieldDetails.displayLabel = '';
      this.fieldDetails.referenceName = '';
      this.fieldDetails.defaultValue = '';
      this.fieldDetails.customValidation = '';
      this.fieldDetails.fieldType = {};
      this.isInvalidRegex = false;
    },
  },
  created() {
    this.fieldDetails.fieldType = this.selectedFieldType;
  }
}
</script>

<style lang="scss">
  @import '../assets/scss/_mixins';

  .field-details {
    @include default-padding;
    flex-grow: 2;
    overflow-y: scroll;
  }

  .field-details-section,
  .selected-field-type {
    display: flex;
    justify-content: space-between;
  }

  .column {
    margin-right: 20px;

    > div {
      margin-bottom: 20px;
    }
  }

  .selected-field-type {
    label {
      margin-bottom: 10px;
    }

    input {
      margin-bottom: 5px;
    }
  }

  .error {
    color: red;
    margin-top: 15px;
  }
</style>
