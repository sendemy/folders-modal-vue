<script setup lang="ts">
import FolderModalTrigger from '@/components/FolderModalTrigger.vue'
import Modal from '@/components/Modal.vue'
import { ref } from 'vue'

const showModal = ref(false)
const selectedFolderId = ref<number | null>(null)

function handleFolderSelect(id: number) {
	selectedFolderId.value = id
	console.log('Selected folder id: ', id)
}
</script>

<template>
	<main>
		<FolderModalTrigger v-model="showModal" />

		<Modal
			title="Дерево папок"
			@select="handleFolderSelect"
			v-model="showModal"
			v-if="showModal"
		/>
	</main>
</template>

<style scoped>
main {
	height: 100vh;
	display: flex;
	justify-content: center;
	align-items: center;
}
</style>
