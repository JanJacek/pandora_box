<template>
  <div class="card">
    <div class="content">
      <h2>
        <slot name="header">Do you want to accept?</slot>
      </h2>
      <p class="caption">{{ caption }}</p>
    </div>
    <div class="actions">
      <button
        :class="['btn', revert ? 'black' : 'white']"
        @click="handleReject"
      >
        Reject
      </button>
      <button
        :class="['btn', revert ? 'white' : 'black']"
        @click="handleAccept"
      >
        Accept changes
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits } from "vue";

defineProps({
  caption: String,
  revert: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits(["reject", "accepted"]);

function handleReject(): void {
  emit("reject");
}
async function handleAccept(): void {
  try {
    const response = await fetch("https://catfact.ninja/fact");
    const data = await response.json();
    console.log("Cat Fact:", data.fact);
    setTimeout(() => {
      emit("accepted");
    }, 150);
  } catch (error) {
    console.error("Some fetch data error:", error);
  }
}
</script>

<style scoped lang="scss">
$background-light-blue: #f4ffff;
$white: #ffffff;
$black: #000000;
$text-opacity: 0.56;
$button-radius: 8px;

.card {
  max-width: 440px;
  padding: 32px;
  background-color: $background-light-blue;
  border: 1px solid #0000001a;
  border-radius: 16px;
  display: flex;
  flex-direction: column;
  gap: 35px;
  text-align: center;

  // The line-height in the project was not standard.
  .content {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
  }
  h2 {
    margin: 0px;
    padding: 0px;
  }
  p {
    margin: 0px;
    padding: 0px;
    font-weight: 400;
  }
  h2 {
    line-height: 29.05px;
  }
  p {
    line-height: 22.4px;
  }
  .caption {
    opacity: $text-opacity;
  }
  .actions {
    display: flex;
    justify-content: center;
    gap: 20px;
    min-width: 376px;
  }
  .btn {
    width: 160px;
    height: 48px;
    padding: 14px 20px;
    border-radius: $button-radius;
    border: 1px solid $black;
    font-weight: 500;
    line-height: 19.36px;
    font-size: 16px;

    &.white {
      background-color: $white;
    }

    &.black {
      background-color: $black;
      color: $white;
    }
  }
  .btn:active {
    transform: scale(0.95);
  }
}
</style>
