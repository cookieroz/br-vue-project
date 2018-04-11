<template>
  <div class="field-sections">
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
          @click="selectedFieldType = fieldType"
          :class="{ 'active-tab': selectedFieldType == fieldType }">
          {{ fieldType.name }}
        </li>
        </ul>
      </div>
    </div>
    <keep-alive>
      <field-details :selectedFieldType="selectedFieldType"></field-details>
    </keep-alive>
  </div>
</template>

<script>
// Imports
import FieldDetails from './FieldDetails.vue';
// import FieldTypes from './components/FieldTypes.vue';
// import FieldDetails from './components/FieldDetails.vue';

export default {
  props: {
    fieldTypes: {
      type: Array,
      required: true
    }
  },
  components: {
    'field-details': FieldDetails
    // 'field-groups': FieldGroups,
    // 'field-tags': FieldTags
  },
  data () {
    return {
      search: '',
      selectedFieldType: {}
    }
  },
  methods: {
  },
  created() {
    this.fieldTypes;
    this.selectedFieldType = this.fieldTypes[0];
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
.field-sections {
  display: flex;
}

.field-types {
  flex-grow: 1;
  margin-right: 1em;
}

.active-tab {
  color: cornflowerblue;
  text-transform: uppercase;
}
</style>
