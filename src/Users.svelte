<script lang="ts">
    import {usersStore} from './stores';
    import UserList from './UserList.svelte';

    type User = {
        login: string,
        avatar_url: string,
        showDetails: boolean
    }

    async function getUsersAsync(): Promise<User[]> {
        const res = await fetch('https://api.github.com/users?login=Shannarra');
        const users = await res.json();
        
        if (res.ok) {
            usersStore.set(users);
            return users;
        }
        throw new Error(users);
    }

    $: allUsers = getUsersAsync();

    export let allUsersList: User[];

</script>

<main class="container">
    <section class="row justify-content-md-center">
        <aside class="col-sm-1 col-lg-2">
        </aside>
        <article class="col-md-auto shadow mb-5">
            {#if allUsersList}
                <UserList usersToPrint={allUsersList} />
            {:else}
                {#await allUsers then users}
                    <UserList usersToPrint={users} />
                #{/await}
            {/if}
        </article>
        <aside class="col-sm-1 col-lg-2">
        </aside>
    </section>
</main>