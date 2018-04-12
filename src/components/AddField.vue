<template>
  <div id="add-field">
    <h2 class="page-title">Commercial Property - Add Field</h2>
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
      <div class="save-field btn" @click="saveFieldItem">
        Save Changes
      </div>
      <div class="no-add-field-buttons">
        <div class="cancel-field btn" @click="resetForm">
          Cancel
        </div>
        <div class="delete-field btn" @click="resetForm">
          Delete
        </div>
      </div>
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

<style lang="scss">
  @import '../assets/scss/_mixins';

  #add-field {
    display: flex;
    flex-direction: column;
    height: calc(100vh - 60px);
    padding: 1em;

    .page-title {
      font-size: 1.8em;
      font-weight: lighter;
      margin-bottom: 1rem;
    }
  }

  .add-field-sections {
    @include round-accent-border;
    display: flex;
    font-weight: lighter;
    overflow: hidden;

    h3 {
      font-size: 1.2rem;
      font-weight: 600;
      margin-bottom: 1rem;
    }

    .field-label {
      font-weight: 500;
    }
  }

  .add-field-controls {
    display: flex;
    padding: 1em 0;
    justify-content: space-between;

    .btn {
      @include round-accent-border;
      cursor: pointer;
      display: inline-block;
      height: 15px;
      padding: 5px;
    }
  }
</style>
