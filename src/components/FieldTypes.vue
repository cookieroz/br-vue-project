<template>
  <div class="field-sections">
    <div class="field-types">
      <h3>Field types section</h3>
      <div class="filter-field-types">
        filter fields go here
      </div>
      <div class="field-types-section">
        field type options go here
        <ul>
          <li
          v-for="fieldType in fieldTypes"
          @click="selectedFieldType = fieldType"
          :class="{ 'active-tab': selectedFieldType == fieldType }">
          {{ fieldType.name }}
        </li>
        </ul>
      </div>
    </div>
    <field-details v-bind:selectedFieldType="selectedFieldType"></field-details>
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
      selectedFieldType: {}
    }
  },
  methods: {
    // post: function(){
    //   this.$http.post('http://jsonplaceholder.typicode.com/posts', {
    //     title: this.blog.title,
    //     body: this.blog.content,
    //     userId: 1
    //   }).then(function(data){
    //     console.log(data);
    //     this.submitted = true;
    //   });
    // }
  },
  created() {
    this.fieldTypes;
    this.selectedFieldType = this.fieldTypes[0];
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
