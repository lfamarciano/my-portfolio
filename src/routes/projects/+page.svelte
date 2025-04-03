<svelte:head>
  <title>My projects</title>
</svelte:head>

<script>
    import Pie from '$lib/Pie.svelte';
    import projects from "$lib/projects.json";
    import Project from "$lib/Project.svelte";
    import * as d3 from 'd3';
    // let rolledData = d3.rollups(projects, v => v.length, d => d.year);
    let pieData;

    $: {
        // Initialize to an empty object every time this runs
        pieData = {};
        
        // Calculate rolledData and pieData based on filteredProjects here
        let rolledData = d3.rollups(filteredProjects, v => v.length, d => d.year);

        // We don't need 'let' anymore since we already defined pieData
        pieData = rolledData.map(([year, count]) => {
            return { value: count, label: year };
        });
    }

    let selectedYearIndex = -1;
    let selectedYear;
    $: selectedYear = selectedYearIndex > -1 ? pieData[selectedYearIndex].label : null;

    let query = "";
    $: filteredProjects = projects.filter(project => {
        let values = Object.values(project).join("\n").toLowerCase();
        return values.includes(query.toLowerCase());
    });
    $: filteredByYear = filteredProjects.filter(project => {
        if (selectedYear) {
            return project.year === selectedYear;
        }

        return true;
    });
</script>

<!-- <pre>{ JSON.stringify(projects, null, "\t") }</pre>   -->

<h1>{ projects.length} Projects</h1>

<Pie data={pieData} bind:selectedIndex={selectedYearIndex} />

<input type="search" bind:value={query} aria-label="Search projects" placeholder="🔍 Search projects..." />

<div class="projects">
    {#each filteredByYear as p}
        <Project data={p}/>
      <!-- <article>
        <h2>{p.title}</h2>
        <img src={p.image} alt="" />
        <p>
            {p.description}
        </p>
      </article> -->
    {/each}
</div>
  

<!-- .projects>article*6>h2>lorem4^img[src="https://i.etsystatic.com/iap/a0f246/5502938083/iap_640x640.5502938083_69958kp0.jpg"]+p>lorem -->
<!-- <div class="projects">
    <article>
        <h2>Lorem ipsum dolor sit.</h2>
        <img src="https://i.etsystatic.com/iap/a0f246/5502938083/iap_640x640.5502938083_69958kp0.jpg" alt="">
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus nesciunt reiciendis possimus dicta doloremque amet sunt aspernatur deserunt sequi! Est hic nesciunt libero natus modi earum maiores aut cum incidunt.</p>
    </article>
    <article>
        <h2>Voluptatibus sint eos consequuntur.</h2>
        <img src="https://i.etsystatic.com/iap/a0f246/5502938083/iap_640x640.5502938083_69958kp0.jpg" alt="">
        <p>Quasi et culpa suscipit, alias quaerat fuga natus eos nulla cupiditate cumque eum voluptatem repellendus dignissimos aut fugiat harum ducimus quibusdam corporis, molestiae expedita ullam hic. Debitis in fugiat nam?</p>
    </article>
    <article>
        <h2>Ab, tenetur aperiam! Id?</h2>
        <img src="https://i.etsystatic.com/iap/a0f246/5502938083/iap_640x640.5502938083_69958kp0.jpg" alt="">
        <p>Cupiditate quibusdam repellat excepturi facilis aperiam, illum alias architecto aspernatur culpa in a mollitia non laboriosam, odio veritatis totam eum et tenetur quidem nemo inventore. Eos sint quia similique? Similique?</p>
    </article>
    <article>
        <h2>Omnis perferendis doloribus qui!</h2>
        <img src="https://i.etsystatic.com/iap/a0f246/5502938083/iap_640x640.5502938083_69958kp0.jpg" alt="">
        <p>Blanditiis eos perferendis, cupiditate accusantium vero adipisci itaque, animi eius voluptatum dolore sapiente ipsum omnis vel in cum nesciunt repellendus a error! Vero ducimus amet fugiat praesentium. Vero, asperiores numquam.</p>
    </article>
    <article>
        <h2>Omnis totam assumenda maiores!</h2>
        <img src="https://i.etsystatic.com/iap/a0f246/5502938083/iap_640x640.5502938083_69958kp0.jpg" alt="">
        <p>Error ullam laboriosam nostrum eos soluta mollitia reprehenderit nulla eaque, cumque et voluptates, voluptatibus adipisci, quod eligendi dolorem asperiores tempore laborum laudantium cupiditate provident cum! Possimus ex similique odio autem?</p>
    </article>
    <article>
        <h2>Qui consequuntur dolore quis?</h2>
        <img src="https://i.etsystatic.com/iap/a0f246/5502938083/iap_640x640.5502938083_69958kp0.jpg" alt="">
        <p>Tempore, culpa consequatur voluptatem quam, repellat inventore alias nam ut incidunt obcaecati qui neque eaque illum nostrum totam ipsa quae quaerat sint quis reiciendis omnis natus placeat quibusdam? Ut, assumenda.</p>
    </article>
</div>  -->