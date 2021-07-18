<script>
	import { App } from '@capacitor/app';
	App.addListener('backButton', () => {
		window.history.back();
	});
</script>

<slot/>
