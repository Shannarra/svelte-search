<script lang="ts">
    export let usersToPrint: any[];
</script>

<section>
    {#each usersToPrint as user}
        <div class="p-2 col col-lg-12">
            <div class="h2 row">
                <img class="rounded-circle img-fluid" width="100" height="100" src={user.avatar_url} alt="avatar" />
                <a class="my-auto font-semibold ml-2" href="https://github.com/{user.login}">{user.login}</a>
            </div>
        </div>
    {/each}
</section>