<script setup>
import ApplicationLogo from '@/Components/ApplicationLogo.vue';
</script>

<template>
	<div>
		<button v-if="$page.props.user.permissions.includes('create roles')">
			Manage Roles
		</button>
		<button v-if="$page.props.user.permissions.includes('create lessons')">
			Manage Lessons
		</button>
	</div>
</template>

<style>
button {
	background-color: #4caf50; /* Green */
	border: none;
	color: white;
	padding: 15px 32px;
	margin: 10px;
	text-align: center;
	text-decoration: none;
	display: inline-block;
	font-size: 16px;
}
</style>
