<template>
  <div
    class="tw-w-full tw-absolute tw-top-1/2 -tw-translate-x-1/2 -tw-translate-y-1/2 tw-transition-all tw-duration-300"
    :style="{ left: isCurrentStep ? '50%' : isNextStep ? '200%' : '-100%' }"
  >
    <div
      class="tw-w-full tw-p-4 tw-rounded-lg container-item tw-overflow-hidden"
    >
      <video
        :src="src"
        :autoplay="value == 0"
        class="tw-rounded-lg container-item__media tw-mx-auto"
        ref="video"
      />
    </div>
    <div class="tw-flex tw-justify-center tw-items-center">
      <button
        class="tw-text-white tw-px-5 tw-py-4 tw-border tw-border-white tw-rounded-lg hover:tw-bg-white hover:tw-text-black tw-uppercase tw-text-sm tw-font-medium tw-transition-all tw-duration-300 tw-tracking-wider"
        @click="next"
      >
        {{ totalCount - 1 == value ? "Finish" : "Next" }}
      </button>
    </div>
  </div>
</template>

<script lang="ts" setup>
const props = defineProps<{
  value: number | string;
  src: string;
}>();

const modelValue = inject<Ref<number | string>>("model-value", ref(0));
const next = inject("next", () => {});
const register = inject("register", () => {});
const totalCount = inject<Ref<number>>("total-count", ref(0));
const video = ref<HTMLVideoElement | null>(null);

const isCurrentStep = computed(() => {
  return Number(modelValue.value) === Number(props.value);
});

const isNextStep = computed(() => {
  return Number(modelValue.value) + 1 === Number(props.value);
});

const isLastStep = computed(() => {
  return Number(modelValue.value) === Number(props.value) - 1;
});

watch(
  () => modelValue.value,
  (value) => {
    if (props.value == value) {
      video.value?.play();
    } else {
      video.value?.pause();
    }
  }
);

register();
</script>

<style scoped>
.container-item {
  max-height: 80vh;
}

.container-item__media {
  max-height: calc(80vh - 64px);
}
</style>
