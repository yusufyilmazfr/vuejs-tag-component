<template>
  <div>
    <Tags v-model="tags" color="warning" />
    {{ tags }}
  </div>
</template>

<script>
import Tags from "./components/Tags";

export default {
  data() {
    return {
      tags: "vue,react,angular"
    };
  },
  components: {
    Tags
  }
};
</script>