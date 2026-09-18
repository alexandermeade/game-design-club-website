<script>
    let userid = $state("");
    let user = $state(null);
    let loading = $state(false);
    let error = $state(null);

    async function getData(id) {
        const response = await fetch(`http://127.0.0.1:8080/user/${id}`);
        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }
        return response.json();
    }

    async function setUser() {
        loading = true;
        error = null;
        try {
            user = await getData(userid);
        } catch (err) {
            error = err.message;
            user = null;
        } finally {
            loading = false;
        }
    }
</script>

<div>
    <input bind:value={userid}>
    <button onclick={setUser}>get user</button>

    {#if loading}
        <p>Loading...</p>
    {:else if error}
        <p style="color: red">{error}</p>
    {:else if user}
        <pre>{JSON.stringify(user, null, 2)}</pre>
    {/if}
</div>
