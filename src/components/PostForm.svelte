<script>
    import { createEventDispatcher } from 'svelte';

    export let editingPost;

    const dispatch = createEventDispatcher();

    $: title = editingPost.title;
    $: body = editingPost.body;
    let isLoading = false;

    const apiBaseUrl = 'https://ndb99xkpdk.execute-api.eu-west-2.amazonaws.com/dev';

    async function onSubmit(event) {
        event.preventDefault();

        if (title.trim() === '' || body.trim() === '') return;

        const newPost = { title, body };
        let url, method;

        if (editingPost.id) {
            url = `${apiBaseUrl}/post/${editingPost.id}`;
            method = 'PUT';
        } else {
            url = `${apiBaseUrl}/post/`;
            method = 'POST';
        }

        try {
            isLoading = true;
            const res = await fetch(url, {
                method,
                body: JSON.stringify(newPost)
            })

            const post = await res.json();

            dispatch('postCreated', post);
        } catch (error) {
            console.log(error);
        }

        isLoading = false;
    }
</script>

<style>
    form {
        margin: 50px;
    }

    .progress {
        margin: 100px 0;
    }
</style>

{#if isLoading}
    <div class="progress">
        <div class="indeterminate"></div>
    </div>
{:else}
    <form on:submit={onSubmit}>
        <div class="input-field">
            <label for="title" class="">Title</label>
            <input type="text" bind:value={editingPost.title}/>
        </div>
        <div class="input-field">
            <label for="title" class="">Body</label>
            <input type="text" bind:value={editingPost.body}/>
        </div>
        <button type="submit" class="waves-effect waves-light btn">
            {editingPost.id ? "Update" : "Add"}
        </button>
    </form>
{/if}