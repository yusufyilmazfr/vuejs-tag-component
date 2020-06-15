<template>
  <div :class="currentTheme" class="tag">
    <span class="text">{{ tag }}</span>
    <span @click="$emit('removeOneTag',index)" class="remove">X</span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentTheme: "default"
    };
  },

  props: {
    tag: {
      required: true
    },
    index: {
      required: true
    },
    color: {
      required: false
    }
  },
  created() {
    if (this.color) {
      this.currentTheme = this.color;
    }
  }
};
</script>

<style scoped>
.remove {
  font-size: 12px;
  cursor: pointer;
}

.default {
  background-color: #ccc;
}

.primary {
  background-color: #007bff;
  color: #fff;
}
.secondary {
  background-color: #6c757d;
  color: #fff;
}
.success {
  background-color: #28a745;
  color: #fff;
}
.danger {
  background-color: #dc3545;
  color: #fff;
  color: #fff;
}
.warning {
  background-color: #ffc107;
  color: #000;
}
.info {
  background-color: #17a2b8;
  color: #fff;
}
.light {
  background-color: #343a40;
  color: #000;
}
</style>