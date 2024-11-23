<script setup lang="ts">
import Button from '@/components/Button.vue'
import FolderTree from '@/components/FolderTree.vue'
import mockFolderData from '@/data/mockFolderData.json'
import { ref } from 'vue'

const props = defineProps<{
	title: string
	modelValue: boolean
}>()
const emit = defineEmits<{
	(event: 'update:modelValue', value: boolean): void
	(event: 'select', folderId: number): void
}>()

const selectedFolderId = ref<number | null>(null)

function closeModal() {
	emit('update:modelValue', false)
}

function handleFolderSelect(id: number | null) {
	selectedFolderId.value = id
}

function confirmSelection() {
	if (selectedFolderId.value !== null) {
		emit('select', selectedFolderId.value)
	}

	closeModal()
}
</script>

<template>
	<div class="modal-overlay" @click.self="closeModal">
		<div class="modal-wrapper">
			<div class="modal-content">
				<h2 class="modal-content__title">{{ title }}</h2>
				<FolderTree
					:children="mockFolderData"
					:on-select="handleFolderSelect"
					:currentSelectedFolderId="selectedFolderId"
				/>
			</div>
			<div class="modal-buttons">
				<Button label="ОК" class="modal-ok-btn" @click="confirmSelection" />
				<Button label="Закрыть" @click="closeModal" />
			</div>
		</div>
	</div>
</template>

<style scoped>
.modal-overlay {
	position: fixed;
	top: 0;
	left: 0;
	width: 100vw;
	height: 100vh;
	background-color: rgba(0, 0, 0, 0.4);
	display: flex;
	justify-content: center;
	align-items: center;
	z-index: 50;
}

.modal-wrapper {
	display: flex;
	flex-direction: column;
	gap: 2rem;
	width: 300px;
	padding: 1.25rem;
	border-radius: 0.5rem;
	text-align: center;
	background: white;
}

.modal-buttons {
	display: flex;
	flex-direction: row;
	justify-content: space-around;
	gap: 2rem;
}

.modal-content__title {
	margin-bottom: 1rem;
}
</style>
