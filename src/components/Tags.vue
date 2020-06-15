<template>
  <div class="tag-container">
    <div class="tags">
      <app-tag
        v-for="(tag, index) in tags"
        :key="index"
        :tag="tag"
        :index="index"
        :color="color"
        @removeOneTag="removeTag($event)"
      ></app-tag>
      <input @keydown.backspace="removeTagWhenPressedBackspace" @keydown.enter="addTag" type="text" />
    </div>
    <div v-if="hasError" :style="{marginTop: '10px', color:'red'}">{{ errorMessage }}</div>
  </div>
</template>

<script>
import Tag from "./Tag";

export default {
  data() {
    return {
      tags: [],
      errorMessage: "This tag already exist!",
      hasError: false,
      currentTheme: null
    };
  },

  methods: {
    addTag(event) {
      let text = event.target.value;

      let isMatched = false;

      if (text.length > 0) {
        this.tags.forEach(tag => {
          if (text.toLowerCase().trim() === tag.toLowerCase()) {
            isMatched = true;
            this.hasError = true;
          }
        });

        if (!isMatched) {
          this.tags.push(text);
          event.target.value = "";
          this.hasError = false;
        }
      }
    },
    removeTag(index) {
      this.tags.splice(index, 1);
    },

    removeTagWhenPressedBackspace(event) {
      if (event.target.value.length === 0) {
        this.tags.pop();
      }
    }
  },

  props: {
    value: {
      required: false,
      type: String
    },
    color: {
      required: false,
      type: String
    }
  },

  components: {
    appTag: Tag
  },

  created() {
    this.tags = this.value.split(",");
  },
  watch: {
    tags() {
      this.$emit("input", this.tags.join(","));
    }
  }
};
</script>

<style scoped>
.tags {
  font-family: sans-serif;
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  border: 1px solid #ddd;
  border-radius: 5px;
  padding: 10px;
  font-size: 14px;
}

.tags * {
  font-size: 14px;
}

.tags input {
  width: 70px;
  height: 20px;
  margin-top: 5px;
  outline: none;
}

.tag {
  border: 1px solid #ddd;
  padding: 5px 10px;
  margin-right: 5px;
  margin-left: 5px;
  margin-top: 5px;
  border-radius: 5px;
}
</style>