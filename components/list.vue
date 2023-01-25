<script lang="ts" setup>

import { useSlots, computed, withDefaults,defineProps } from 'vue';

withDefaults(defineProps<{
	items: unknown[]; // The items to list
	nick?: string; // The items nickname defines the name under which items and slot will be accessible
}>(), {
	nick: 'item'
});

// The list slots
const slots = useSlots();

// Is there any before slot ?
const showBefore = computed(() => {
	return !!slots.before;
});

// Is there any after slot ?
const showAfter = computed(() => {
	return !!slots.after;
});

</script>

<template>
	<ul>

		<li v-if="showBefore">
			<slot name="before" />
		</li>

		<template
			v-for="(item, index) in items"
			:key="index"
		>

			<li>
				<slot :name="nick" v-bind="{ [nick]: item, index }"/>
			</li>

		</template>

		<li v-if="showAfter">
			<slot name="after" />
		</li>

	</ul>
</template>
