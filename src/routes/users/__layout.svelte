<script lang="ts">
	import { page } from '$app/stores';

	const active_classes =
		'text-center block border border-blue-500 rounded py-2 px-4 bg-blue-500 hover:bg-blue-700 text-white';
	const inactive_classes =
		'text-center block border border-white rounded hover:border-gray-200 text-blue-500 hover:bg-gray-200 py-2 px-4';
	const disabled_classes = 'block py-2 px-4 text-gray-400 cursor-not-allowed';

	let active = '';
	function refresh() {
		switch ($page.url.pathname) {
			case '/users':
			case '/users/add':
				active = 'add';
				break;
			case '/users/delete':
				active = 'delete';
				break;
			case '/users/update':
				active = 'update';
				break;
			default:
				active = 'add';
		}
	}
	refresh();

	$: if ($page.url.pathname) refresh();
</script>

<ul class="flex">
	<li class="flex-1 mr-2">
		<a class={active == 'add' ? active_classes : inactive_classes} href="/users/add">Add</a>
	</li>
	<li class="flex-1 mr-2">
		<a class={active == 'update' ? active_classes : inactive_classes} href="/users/update">Update</a
		>
	</li>
	<li class="flex-1 mr-2">
		<a class={active == 'delete' ? active_classes : inactive_classes} href="/users/delete">Delete</a
		>
	</li>
</ul>

<slot />
