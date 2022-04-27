<template>
<MkPagination ref="pagingComponent" :pagination="pagination">
	<template #empty>
		<div class="_fullinfo">
			<img src="https://erisly.social/files/b02ec5a9-b3ba-4f24-a40e-156ba23a3b0e" class="_ghost"/>
			<div>{{ $ts.noUsers }}</div>
		</div>
	</template>

	<template #default="{ items: users }">
		<div class="efvhhmdq">
			<MkUserInfo v-for="user in users" :key="user.id" class="user" :user="user"/>
		</div>
	</template>
</MkPagination>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import MkUserInfo from '@/components/user-info.vue';
import MkPagination from '@/components/ui/pagination.vue';
import { Paging } from '@/components/ui/pagination.vue';
import { userPage } from '@/filters/user';

const props = defineProps<{
	pagination: Paging;
	noGap?: boolean;
}>();

const pagingComponent = ref<InstanceType<typeof MkPagination>>();
</script>

<style lang="scss" scoped>
.efvhhmdq {
	display: grid;
	grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
	grid-gap: var(--margin);
}
</style>
