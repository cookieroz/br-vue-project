<template>
  <div id="add-field">
    <h2>add field section</h2>
    <div class="add-field-sections">
      <field-types
        ref="fieldTypeComponent"
        v-on:selectedFieldType="updateSelectedFieldType($event)"
        :selectedFieldType="fieldItem.selectedFieldType">
      </field-types>
      <div class="field-details">
        <h3>Field Details Section</h3>
        <div class="field-details-section">
          <div class="field-type-tags-section">
            <field-details
              ref="fieldDetailsComponent"
              v-on:fieldDetails="getFieldDetails($event)"
              :selectedFieldType="fieldItem.selectedFieldType">
            </field-details>
            <field-tags ref="fieldTagComponent"></field-tags>
          </div>
          <field-groups
            ref="fieldGroupComponent"
            v-on:selectedFieldGroup="getFieldGroup($event)">
          </field-groups>
        </div>
      </div>
    </div>

    <div class="add-field-controls">
      <button @click="saveFieldItem">Save Changes</button>
      <button @click="resetForm">Cancel</button>
    </div>
  </div>
</template>

<script>
// Imports
import FieldTypes from './FieldTypes.vue';
import FieldDetails from './FieldDetails.vue';
import FieldTags from './FieldTags.vue';
import FieldGroups from './FieldGroups.vue';

export default {
  components: {
    'field-types': FieldTypes,
    'field-details': FieldDetails,
    'field-tags': FieldTags,
    'field-groups': FieldGroups
  },
  data () {
    return {
      fieldItem: {
        selectedFieldType: {},
        fieldGroups: [],
        fieldDetails: {},
      }
    }
  },
  methods: {
    updateSelectedFieldType: function(selectedFieldType) {
      console.log(selectedFieldType);
      this.fieldItem.selectedFieldType = selectedFieldType;
    },

    getFieldGroup: function(selectedFieldGroup) {
      console.log(selectedFieldGroup);
      this.fieldItem.fieldGroups.push(selectedFieldGroup);
    },

    getFieldDetails: function(fieldDetails) {
      this.fieldItem.fieldDetails = fieldDetails;
    },

    resetForm: function() {
      this.fieldItem.selectedFieldType = {};
      this.fieldItem.fieldGroups = [];
      this.fieldItem.fieldDetails = {};
      this.$refs.fieldDetailsComponent.resetFieldDetails();
      this.$refs.fieldGroupComponent.resetFieldGroups();
      this.$refs.fieldTypeComponent.showFirstFieldType();
      this.$refs.fieldTagComponent.resetFieldTags();
    },

    saveFieldItem: function() {
      this.$refs.fieldDetailsComponent.sendFieldDetails();
      console.log(this.fieldItem);
      this.resetForm();
    }
  }
}
</script>

<style>
.add-field-sections {
  display: flex;
}
</style>
