<template>
  <div
    class="tw-text-white tw-h-screen tw-flex tw-flex-col tw-items-center tw-justify-center tw-relative"
  >
    <div
      v-if="state === 'start'"
      class="tw-flex tw-items-center tw-justify-center tw-flex-col"
    >
      <button
        class="tw-text-white tw-px-5 tw-py-4 tw-border tw-border-white tw-rounded-lg hover:tw-bg-white hover:tw-text-black tw-uppercase tw-text-sm tw-font-medium tw-transition-all tw-duration-300 tw-tracking-wider"
        @click="onStart"
      >
        Get started
      </button>
    </div>

    <client-only>
      <CarouselGroup
        v-if="state === 'carousel'"
        v-model="step"
        @finish="onFinish"
      >
        <CarouselItem
          value="0"
          src="https://mbnztbzktykfjsacwhvk.supabase.co/storage/v1/object/public/videos/video-1.mp4?t=2024-12-10T17%3A56%3A08.621Z"
        >
        </CarouselItem>
        <CarouselItem
          value="1"
          src="https://mbnztbzktykfjsacwhvk.supabase.co/storage/v1/object/public/videos/video-2.mp4?t=2024-12-10T17%3A56%3A31.963Z"
        >
        </CarouselItem>
        <CarouselItem
          value="2"
          src="https://mbnztbzktykfjsacwhvk.supabase.co/storage/v1/object/public/videos/video-3.mp4?t=2024-12-10T17%3A56%3A38.488Z"
        >
        </CarouselItem>
      </CarouselGroup>
    </client-only>
  </div>
</template>

<script setup lang="ts">
import CarouselGroup from "@/components/CarouselGroup.vue";
import CarouselItem from "@/components/CarouselItem.vue";

const state = ref<"start" | "carousel">("start");

function onStart() {
  state.value = "carousel";
}

const step = ref(0);
function onFinish() {
  state.value = "start";
}
</script>
