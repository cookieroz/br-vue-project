<template>
  <div class="field-tags">
    <h3>Tags</h3>

    <div class="field-tags-section">
      <div class="tag-groups-section">
        <p class="field-label">Tag Group</p>
        <ul>
          <li
            v-for="fieldTag in fieldTags"
            @click="onTagClick(fieldTag)"
            :class="{ 'active-tab': selectedFieldTag == fieldTag }">
            {{ fieldTag.groupName }}
          </li>
        </ul>
      </div>

      <div class="tags-section">
        <p class="field-label">Tags</p>
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
    },

    resetFieldTags: function() {
      this.selectedFieldTag = {};
      this.showTags = null;
    }
  }
}
</script>

<style lang="scss">
  @import '../assets/scss/_mixins';
  .field-tags-section {
    display: flex;

    li {
      @include round-accent-border;
      background-color: $tag-button-background-color;
      color: $accent-text-color;
      display: inline-block;
      font-weight: 500;
      margin: 10px 10px 0 0;
      padding: 5px;
    }
  }

  .tag-groups-section,
  .tags-section {
    flex: 1;
  }

  .no-shown-tags {
    font-style: italic;
    margin-top: 10px;
  }
</style>
