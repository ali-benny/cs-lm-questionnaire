<script setup>
defineProps({
  modelValue: {
    type: Number,
    default: 0,
    required: true,
  },
})

const emit = defineEmits(['update:modelValue'])

function updateRating(value) {
  emit('update:modelValue', Number(value))
}
</script>

<template>
  <div class="rating rating-lg">
    <input
      type="radio"
      :name="`star-rating-${Math.random()}`"
      :class="['mask mask-star-2', modelValue >= 1 ? 'bg-orange-400' : 'bg-base-content/60']"
      value="1"
      :checked="modelValue === 1"
      @change="updateRating(1)"
    />
    <input
      type="radio"
      :name="`star-rating-${Math.random()}`"
      :class="['mask mask-star-2', modelValue >= 1 ? 'bg-orange-400' : 'bg-base-content/60']"
      value="2"
      :checked="modelValue === 2"
      @change="updateRating(2)"
    />
    <input
      type="radio"
      :name="`star-rating-${Math.random()}`"
      :class="['mask mask-star-2', modelValue >= 1 ? 'bg-orange-400' : 'bg-base-content/60']"
      value="3"
      :checked="modelValue === 3"
      @change="updateRating(3)"
    />
    <input
      type="radio"
      :name="`star-rating-${Math.random()}`"
      :class="['mask mask-star-2', modelValue >= 1 ? 'bg-orange-400' : 'bg-base-content/60']"
      value="4"
      :checked="modelValue === 4"
      @change="updateRating(4)"
    />
    <input
      type="radio"
      :name="`star-rating-${Math.random()}`"
      :class="['mask mask-star-2', modelValue >= 1 ? 'bg-orange-400' : 'bg-base-content/60']"
      value="5"
      :checked="modelValue === 5"
      @change="updateRating(5)"
    />
  </div>
</template>
