<script>
export default {
	name: 'LessonsCreate',
};
</script>

<script setup>
import { useForm } from '@inertiajs/vue3';
import AppLayout from '@/Layouts/AppLayout.vue';
import LessonForm from '@/Components/Lessons/Form.vue';

defineProps({
	categories: {
		type: Object,
		required: true,
	},

	levels: {
		type: Object,
		required: true,
	},
});

const form = useForm({
	name: '',
});
</script>

<template>
	<AppLayout>
		<template #header>
			<h1 class="font-semibold text-xl text-gray-800 leading-tight">
				Create Lesson
			</h1>
		</template>

		<div class="py-12">
			<div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
				<div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
					<div class="p-6 border-b border-gray-200">
						<LessonForm
							:form="form"
							:categories="$page.props.categories"
							:levels="$page.props.levels"
							@submit="form.post(route('lessons.store'))"
						/>
					</div>
				</div>
			</div>
		</div>
	</AppLayout>
</template>
