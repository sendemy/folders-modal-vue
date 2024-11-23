<script setup lang="ts">
import { useAttrs } from 'vue'

const { label } = defineProps<{
	label: string
}>()

const attrs = useAttrs()
</script>

<template>
	<button type="button" v-bind="attrs">{{ label }}</button>
</template>

<style scoped>
button {
	cursor: pointer;
	outline: 0;
	display: inline-block;
	font-weight: 400;
	line-height: 1.5;
	text-align: center;
	background-color: transparent;
	border: 1px solid transparent;
	padding: 0.25rem 0.75rem;
	font-size: 1rem;
	border-radius: 0.25rem;
	transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out,
		border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
	color: #0d6efd;
	border-color: #0d6efd;
}

button:hover {
	color: #fff;
	background-color: #0d6efd;
	border-color: #0d6efd;
}
</style>
