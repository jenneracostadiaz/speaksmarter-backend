<script setup>
import { ref } from 'vue';

defineProps({
	collection: {
		type: Array,
		required: true,
	},
});

const currentSelection = ref(1);
const selection = ref([]);
const emit = defineEmits(['onCategories']);

const handleAddToSelection = () => {
	let alreadyExists = false;
	selection.value.forEach((item) => {
		if (item.id === currentSelection.value.id) {
			alreadyExists = true;
			return;
		}
	});
	if (alreadyExists) return;
	selection.value.push(currentSelection.value);
	emit('onCategories', selection.value);
};

const handleRemoveSelection = (index) => {
	selection.value = selection.value.filter((item, i) => i !== index);
	emit('onCategories', selection.value);
};
</script>

<template>
	<div class="flex gap-2">
		<select
			v-model="currentSelection"
			class="flex-1 border-gray-300 focus:border-indigo-500 focus:ring-indigo-500 rounded-md shadow-sm mt-1 block w-full"
		>
			<option v-for="(item, index) in collection" :key="index" :value="item">
				{{ item?.name }}
			</option>
		</select>
		<button
			@click="handleAddToSelection"
			class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-1 px-4 rounded"
		>
			Add
		</button>
	</div>

	<div>
		<ul class="mt-4">
			<li
				v-for="(item, index) in selection"
				:key="index"
				class="my-2 bg-indigo-400 text-white p-2 rounded flex justify-between items-center"
			>
				{{ item.name }}
				<span
					@click="handleRemoveSelection(index)"
					class="cursor-pointer text-slate-50 text-xs font-bold ml-2 hover:text-red-500 px-2"
					>&times;</span
				>
			</li>
		</ul>
	</div>
</template>
