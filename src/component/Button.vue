<script setup lang="ts">
interface Props {
  title: string;
  variant?: "primary" | "success" | "danger" | "default";
}
withDefaults(defineProps<Props>(), {
  title: "Judul Button",
  variant: "default",
});
</script>

<template>
  <button :class="`button ${variant}`">{{ title }}</button>
</template>

<style lang="scss" scoped>
.button {
  background: linear-gradient(135deg, hsl(260 60% 55%), hsl(195 100% 50%));
  padding: 10px 30px;
  border-radius: 10px;
  outline: none;
  border: none;
  font-weight: 600;
  font-size: 16.9;
  max-width: 400px;
  width: 100%;
  cursor: pointer;
}

.default {
  background: #161625;
  color: #a7a8b0;
  border: 3px solid #a7a8b02c;

  &:hover {
    border: 3px solid #0c85b4;
    background: rgba(0, 0, 0, 0);
  }
}

.danger {
  background: #31202d;
  border: 2px solid #832f37;
  color: #716c77;
}

.success {
  background: #1d2e31;
  border: 2px solid #1c7143;
  color: #716c77;
}
</style>
