<template>
  <div id="add-field">
    <h2>add field section</h2>
    <field-types v-bind:fieldTypes="fieldTypes"></field-types>
  </div>
</template>

<script>
// Imports
import FieldTypes from './FieldTypes.vue';

export default {
  components: {
    'field-types': FieldTypes
    // 'field-groups': FieldGroups,
    // 'field-tags': FieldTags
  },
  data () {
    return {
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
      // authors: ['The Net Ninja', 'The Angular Avenger', 'The Vue Vindicator'],
      // submitted: false
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
  }
}
</script>

<style>
</style>
