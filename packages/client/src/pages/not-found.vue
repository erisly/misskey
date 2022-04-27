<template>
<div class="ipledcug">
	<div class="_fullinfo">
		<img src="https://erisly.social/files/71db9da0-b91b-4287-a4be-169c02eb89ca" class="_ghost"/>
		<div>{{ $ts.notFoundDescription }}</div>
	</div>
</div>
</template>

<script lang="ts" setup>
import * as symbols from '@/symbols';
import { i18n } from '@/i18n';

defineExpose({
	[symbols.PAGE_INFO]: {
		title: i18n.ts.notFound,
		icon: 'fas fa-exclamation-triangle',
		bg: 'var(--bg)',
	},
});
</script>
