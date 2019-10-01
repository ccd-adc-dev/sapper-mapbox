<script>
	import { getContext, onMount } from 'svelte';
	import key from '../../mapbox-context-key.js'

	
	const { getMap } = getContext(key);
	const map = getMap();

	export let lat;
	export let lon;
	export let label;

	onMount(async () => {

		const mapboxModule = await import('mapbox-gl');
		const mapbox = mapboxModule.default

		const popup = new mapbox.Popup({ offset: 25 })
			.setText(label);

		const marker = new mapbox.Marker()
			.setLngLat([lon, lat])
			.setPopup(popup)
			.addTo(map);
	})
</script>