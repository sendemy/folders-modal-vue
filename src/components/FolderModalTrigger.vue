<script setup lang="ts">
import Button from '@/components/Button.vue'

const emit = defineEmits<{
	(event: 'update:modelValue', value: boolean): void
}>()

const openModal = () => {
	emit('update:modelValue', true)
}
</script>

<template>
	<div>
		<Button label="Открыть" @click="openModal" />
	</div>
</template>

<style scoped>
div {
	padding: 6rem 9rem;
	border: 1px solid #c6ddff;
}
</style>
