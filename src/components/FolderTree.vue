<script setup lang="ts">
import { defineProps, reactive } from 'vue'
import folderClosedIcon from '../assets/folderClosed.svg'
import folderOpenIcon from '../assets/folderOpen.svg'

interface Folder {
	id: number
	name: string
	children: Folder[]
}

const props = defineProps<{
	children: Folder[]
	onSelect: (id: number | null) => void
	currentSelectedFolderId: number | null
}>()

const expandedFolders = reactive(new Map<number, boolean>())

function toggleListExpand(folderId: number) {
	expandedFolders.set(folderId, !expandedFolders.get(folderId))
}

function isFolderExpanded(folderId: number) {
	return expandedFolders.get(folderId) || false
}
</script>

<template>
	<ul>
		<li v-for="folder in children" :key="folder.id">
			<div>
				<span @click="() => toggleListExpand(folder.id)">
					<img
						:src="
							isFolderExpanded(folder.id) ? folderOpenIcon : folderClosedIcon
						"
						alt="Folder Icon"
						width="16"
						height="16"
					/>
					<span>{{ folder.name }}</span>
				</span>
				<input
					type="checkbox"
					name="checkbox"
					id="checkbox"
					:checked="currentSelectedFolderId === folder.id"
					@click="(e) => onSelect((e.target as HTMLInputElement).checked ? folder.id : null)"
				/>
			</div>
			<ul v-if="isFolderExpanded(folder.id)">
				<FolderTree
					v-if="folder.children.length"
					:children="folder.children"
					:onSelect="onSelect"
					:currentSelectedFolderId="currentSelectedFolderId"
				/>
			</ul>
		</li>
	</ul>
</template>

<style scoped>
ul {
	list-style-type: none;
	padding-left: 1rem;
}

li {
	margin: 0.5rem 0;
	cursor: pointer;
}

img {
	margin-right: 0.3rem;
}

input {
	margin-left: 1rem;
}
</style>
