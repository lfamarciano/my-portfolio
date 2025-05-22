<script>
    import * as d3 from "d3";
    export let lines=[];
    export let width=null;

    let files = [];
    $: files = d3.groups(lines, d => d.file)
                .map(([name, lines]) => ({ name, lines }));

    let svg;
    $: if (svg) {
        const rowHeight = 30;
        const width = 400;
        const height = files.length * rowHeight;
        const groups = d3.select(svg)
            .selectAll('g.file')
            .data(files, d => d.name);
        d3.select(svg)
            .attr('width', width)
            .attr('height', height);
    }
</script>

<svg bind:this={svg}></svg>