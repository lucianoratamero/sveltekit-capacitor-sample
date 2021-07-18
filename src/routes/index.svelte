<script>
	import { onMount } from 'svelte';
	import { Geolocation } from '@capacitor/geolocation';
	import { Filesystem, Directory, Encoding } from '@capacitor/filesystem';

	let fileData, loc;

	async function getCurrentPosition() {
		try {
			const res = await Geolocation.getCurrentPosition();
			loc = res;
		} catch (e) {
			console.log(e);
			loc = {
				coords: {
					latitude: "Couldn't get location data",
					longitude: "Couldn't get location data"
				}
			};
		}
	}

	async function readDummyTextFile() {
		let file;
		try {
			file = await Filesystem.readFile({
				path: 'dummy.txt',
				directory: Directory.Data,
				encoding: Encoding.UTF8
			});
			fileData = file.data;
			return file;
		} catch (e) {
			await Filesystem.writeFile({
				path: 'dummy.txt',
				data: 'This is a dummy text file.',
				directory: Directory.Data,
				encoding: Encoding.UTF8
			});
			readDummyTextFile();
		}
	}

	onMount(async () => {
		readDummyTextFile();
		Geolocation.watchPosition({}, (location) => loc = location);
	});
</script>

<h1>capacitor é lindo e maravilhoso</h1>

<h1>{fileData}</h1>
<div>
	<h2>Geolocation</h2>
	<p>Your location is:</p>
	<p>Latitude: {loc ? loc.coords.latitude : 'Getting location...'}</p>
	<p>Longitude: {loc ? loc.coords.longitude : 'Getting location...'}</p>
</div>

<a href="/about">go to about</a>

<style>
	h1 { color: red }
</style>
