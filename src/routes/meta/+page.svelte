<script>
import * as d3 from "d3";

import { onMount } from "svelte";

let data = [];

onMount(async () => {
    data = await d3.csv("/loc.csv");
});


</script>

<h1>Meta</h1>
<p>This page contains stats about the code of this website.</p>
<p>Total lines of code: {data.length}</p>


