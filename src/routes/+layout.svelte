<script lang="ts">
	import '../app.pcss';
	import { ModeWatcher } from 'mode-watcher';
</script>

<ModeWatcher />

<div class="flex items-center justify-center h-full p-24">
<slot />
</div>