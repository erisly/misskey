<template>
<div
	v-size="{ min: [350, 500] }"
	class="yohlumlk"
	@click.left.stop="onClick"
	@click.middle.stop="onMiddleClick"
	@mousedown.middle.prevent
>
	<MkAvatar class="avatar" :user="note.user"/>
	<div class="main">
		<XNoteHeader ref="header" class="header" :note="note" :mini="true"/>
		<div class="body">
			<p v-if="note.cw != null" class="cw">
				<span v-if="note.cw != ''" class="text">{{ note.cw }}</span>
				<XCwButton v-model="showContent" :note="note"/>
			</p>
			<div v-show="note.cw == null || showContent" class="content">
				<MkNoteSubNoteContent class="text" :note="note"/>
			</div>
		</div>
	</div>
</div>
</template>

<script lang="ts" setup>
import { } from 'vue';
import * as misskey from 'misskey-js';
import XNoteHeader from './note-header.vue';
import MkNoteSubNoteContent from './sub-note-content.vue';
import XCwButton from './cw-button.vue';

const props = defineProps<{
	note: misskey.entities.Note;
	pinned?: boolean;
}>();

const showContent = $ref(false);

const header = $ref<{anchor?: HTMLAnchorElement}>()
const anchor = $computed(() => header?.anchor)

const onClick = (ev: MouseEvent) => {
  if (!window.getSelection()?.toString()) {
		ev.preventDefault();
		anchor?.click();
	}
};
const onMiddleClick = (ev: MouseEvent) => {
  ev.preventDefault();
  window.open(anchor?.href, "_blank");
};
</script>

<style lang="scss" scoped>
.yohlumlk {
	display: flex;
	margin: 0;
	padding: 0;
	overflow: clip;
	font-size: 0.95em;
	cursor: pointer;

	&.min-width_350px {
		> .avatar {
			margin: 0 10px 0 0;
			width: 44px;
			height: 44px;
		}
	}

	&.min-width_500px {
		> .avatar {
			margin: 0 12px 0 0;
			width: 48px;
			height: 48px;
		}
	}

	> .avatar {
		flex-shrink: 0;
		display: block;
		margin: 0 10px 0 0;
		width: 40px;
		height: 40px;
		border-radius: 8px;
	}

	> .main {
		flex: 1;
		min-width: 0;

		> .header {
			margin-bottom: 2px;
		}

		> .body {

			> .cw {
				display: block;
				margin: 0;
				padding: 0;
				overflow-wrap: break-word;

				> .text {
					margin-right: 8px;
				}
			}

			> .content {
				> .text {
					margin: 0;
					padding: 0;
				}
			}
		}
	}
}
</style>
