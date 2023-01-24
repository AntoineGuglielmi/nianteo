<script lang="ts" setup>
const props = withDefaults(defineProps<{
	items: Array<unknown>,
	nick?: string
}>(), {
	nick: 'item'
});
</script>

<template>
	<ul>
		<li
			v-for="(item, index) in items"
		>
			<slot :name="nick" v-bind="{ [nick]: item, index }"></slot>
		</li>
	</ul>
</template>
