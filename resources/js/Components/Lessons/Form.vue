<script>
export default {
	name: 'LessonsForm',
};
</script>

<script setup>
import FormSection from '@/Components/FormSection.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import SecondaryButton from '@/Components/SecondaryButton.vue';
import CollectionSelector from '@/Components/Common/CollectionSelector.vue';
import { ref } from 'vue';

defineProps({
	form: {
		type: Object,
		required: true,
	},

	updating: {
		type: Boolean,
		required: false,
		default: false,
	},
	categories: {
		type: Object,
		required: true,
	},
	levels: {
		type: Object,
		required: true,
	},
});

const categoriesSelected = ref([]);

const onCategories = (_categories) => {
	categoriesSelected.value = _categories;
};

defineEmits(['submit']);
</script>

<template>
	<FormSection @submitted="$emit('submit')">
		<template #title>
			{{ updating ? 'Update Lesson' : 'Create Lesson' }}
		</template>

		<template #description>
			{{ updating ? 'Update the lesson details' : 'Create a new lesson' }}
		</template>

		<template #form>
			<div class="block">
				<InputLabel for="name" value="Name" />
				<TextInput
					id="name"
					v-model="form.name"
					type="text"
					autocomplete="name"
					class="mt-1 block w-full"
				/>
				<InputError :message="$page.props.errors.name" class="mt-2" />
			</div>
			<div class="block">
				<InputLabel for="description" value="Description" />
				<TextInput
					id="description"
					v-model="form.description"
					type="text"
					autocomplete="description"
					class="mt-1 block w-full"
				/>
				<InputError :message="$page.props.errors.description" class="mt-2" />
			</div>
			<div class="block">
				<InputLabel for="content_uri" value="Content uri" />
				<TextInput
					id="content_uri"
					v-model="form.content_uri"
					type="text"
					autocomplete="content_uri"
					class="mt-1 block w-full"
				/>
				<InputError :message="$page.props.errors.content_uri" class="mt-2" />
			</div>

			<div class="block">
				<SecondaryButton class="mt-4" type="button">
					Upload PDF
				</SecondaryButton>
				<InputError :message="$page.props.errors.pdf_uri" class="mt-2" />
			</div>
			<div class="flex gap-4">
				<div class="flex-1 w-full block">
					<InputLabel for="category_id" value="Level" />
					<select
						class="border-gray-300 focus:border-indigo-500 focus:ring-indigo-500 rounded-md shadow-sm mt-1 block w-full"
					>
						<option v-for="level in levels" :value="level.id">
							{{ level.name }}
						</option>
					</select>
					<InputError :message="$page.props.errors.level_id" class="mt-2" />
				</div>
				<div class="flex-1 block">
					<InputLabel for="category_id" value="Category" />
					<CollectionSelector
						name="categories"
						id="categories"
						:collection="categories"
						@onCtegories="onCategories"
					/>
				</div>
			</div>
		</template>

		<template #actions>
			<PrimaryButton>
				{{ updating ? 'Update' : 'Create' }}
			</PrimaryButton>
		</template>
	</FormSection>
</template>
