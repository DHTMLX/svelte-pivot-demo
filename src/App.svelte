<script>
	import Pivot from "./Pivot.svelte";
	import { getData } from "./data.js";

	const {fields, dataset} = getData();
</script>

<Pivot fields={fields} dataset={dataset} />
