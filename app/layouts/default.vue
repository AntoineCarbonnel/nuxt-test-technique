<script lang="ts" setup>
import Header from "~/components/Header.vue";

</script>

<template>
	<Header/>
	<main class="flex justify-center">
		<slot/>
	</main>
</template>

<style>
body {
	background-color: #F7F3F0;
	margin: 0;
	padding: 0;
	font-family: sans-serif;
}
</style>
