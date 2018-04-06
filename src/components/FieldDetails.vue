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
  // data () {
    // return {
    //   blog: {
    //     title: '',
    //     content: '',
    //     categories: [],
    //     author: ''
    //   },
    //   authors: ['The Net Ninja', 'The Angular Avenger', 'The Vue Vindicator'],
    //   submitted: false
    // }
  // },
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
.field-details {
  flex-grow: 2;
}

.field-details-section {
  display: flex;
}
</style>
