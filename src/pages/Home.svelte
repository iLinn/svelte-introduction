<script>
    import { onMount } from 'svelte';

    import Spinner_triangle from '..//layout/Spinner_triangle.svelte';
    import Spinner_dot from '..//layout/Spinner_dot.svelte';

    const apiBaseUrl = 'https://ndb99xkpdk.execute-api.eu-west-2.amazonaws.com/dev';
    let posts = [];

    onMount(async () => {
        const res = await fetch(apiBaseUrl + '/posts');
        posts = await res.json();
    })
</script>

<div class="row">
    {#if posts.length === 0}
        <div class="center">
            <h3>Loading posts...</h3>
            <Spinner_triangle />
            <Spinner_dot />
        </div>
    {:else}
        {#each posts as post}
            <div class="col s6">
                <div class="card">
                    <div class="card-content">
                        <p class="card-title">{post.title}</p>
                        <p>{post.createdAt}</p>
                        <p>{post.body}</p>
                    </div>
                </div>
            </div>
        {/each}
    {/if}
</div>