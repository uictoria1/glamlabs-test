<template>
  <div>
    <slot />
  </div>
</template>

<script lang="ts" setup>
const props = defineProps<{
  modelValue: number | string;
}>();
const emit = defineEmits<{
  (e: "update:model-value", value: number | string): void;
  (e: "finish"): void;
  (e: "next"): void;
}>();

const totalCount = ref(0);

provide("register", () => {
  totalCount.value++;
});
provide("total-count", totalCount);
provide(
  "model-value",
  computed(() => Number(props.modelValue))
);
provide("next", () => {
  const nextValue = Number(props.modelValue) + 1;
  if (nextValue < totalCount.value) {
    emit("update:model-value", nextValue);
    emit("next");
  } else {
    emit("finish");
    emit("update:model-value", 0);
  }
});
</script>
