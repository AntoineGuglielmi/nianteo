<script lang="ts" setup>
import { Ref, ref, useSlots, computed } from 'vue';
export interface Action {
	text: string,
	value: unknown
}

const props = withDefaults(defineProps<{
	actions?: Array<Action>; // The actions triggered by the modal's buttons
	outterExit?: boolean; // Determines if the modal closes if clicked outside body
}>(), {
	actions: [
		{
			text: 'Validate',
			value: true
		},
		{
			text: 'Cancel',
			value: false
		}
	],
	outterExit: false,
});

const openModal: Ref<boolean> = ref(false);
let callback = () => {};

const open = () => {
	openModal.value = true;
	return new Promise((resolve, rej) => {
		callback = resolve;
	});
}

const answer = (value: any) => {
	openModal.value = false;
	callback(value);
}

const close = () => {
	openModal.value = false;
}

const slots = useSlots();

const hasDefault = computed(() => {
	return slots.default !== undefined;
});

defineExpose({
	open,
	answer
});

</script>

<template>
	<div
		class="modal__main"
		v-if="openModal"
		@click.self="outterExit ? close() : null"
	>

		<slot v-if="hasDefault"></slot>

		<slot v-else>

			<div class="modal__inner">

				<div class="modal__body">

					<slot name="title"><h2>Override with #title</h2></slot>
					<slot name="desc"><p>Override with #desc</p></slot>

				</div>

				<div class="modal__actions">

					<slot name="actions">
						<button
							v-for="(action, index) in actions"
							:key="index"
							@click.prevent="answer(action.value)"
						>
							{{ action.text }}
						</button>
					</slot>

				</div>

			</div>

		</slot>

	</div>
</template>
