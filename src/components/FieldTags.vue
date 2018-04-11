<template>
  <div class="field-tags">
    <h3>Tags</h3>
    <h4>Tag Group</h4>
    <ul>
      <li
        v-for="fieldTag in fieldTags"
        @click="onTagClick(fieldTag)"
        :class="{ 'active-tab': selectedFieldTag == fieldTag }">
        {{ fieldTag.groupName }}
      </li>
    </ul>

    <h4>Tags</h4>
    <div class="tags-shown" v-if="showTags">
      <ul>
        <li
          v-for="tag in showTags">
          {{ tag }}
        </li>
      </ul>
    </div>
    <div class="no-shown-tags" v-else>
      Select a tag group to see individual tags.
    </div>

  </div>
</template>

<script>

export default {
  data () {
    return {
      fieldTags: [
        {
          groupName: 'Vinmaster',
          tags: ['car make', 'car model', 'year built']
        },
        {
          groupName: 'ISO',
          tags: ['iso type', 'iso claims', 'iso tag']
        },
        {
          groupName: 'house',
          tags: ['house type', 'number of bedrooms']
        },
      ],
      selectedFieldTag: {},
      showTags: null
    }
  },
  methods: {
    onTagClick: function(fieldTag) {
      this.selectedFieldTag = fieldTag;
      this.showTags = fieldTag.tags;
    }
  }
}
</script>

<style>

</style>
