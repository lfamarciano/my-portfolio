<script>
    export let data = {};
    export let hLevel = 2;
</script>


<div class="projects">
    <article>
        <svelte:element this={"h" + hLevel}>{data.title}</svelte:element>
        <img src={data.image} alt="" />
        <p>
            {data.description}
            <br/>
            {data.year}
        </p>
    </article>
    
</div>

<style>
    p {
        font-size: 0.7em;
    }
    img {
        height: 12em;
    }
</style>
