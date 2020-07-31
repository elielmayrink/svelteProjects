<script>
    import { createEventDispatcher } from 'svelte';

    export let id;
    export let title;
    export let subtitle;
    export let imageUrl;
    export let address;
    export let descriptions;
    export let email;
    export let favorite;
    export let active;
    export let deleteMeet;
    export let isFav;

    const dispatch = createEventDispatcher();
</script>

<article class:active={active === "active"}>
    <header>
        <div>
            <h1>{title}</h1>
            <h2>{subtitle}</h2>
            <p>{address}</p>
        </div>
        <div>
            {#if favorite}
                <p class="favorito">Favorito</p>
            {/if}
        </div>
    </header>
    <div class="image">
        <img src="{imageUrl}" alt="{title}">
    </div>
    <div class="content">
        <p>{descriptions}</p>
    </div>
    <footer>
        <a class="button" href="mailto:{email}">Contact</a>
        <button 
        class:bgFavorite={isFav === "Favorite"} 
        class:bgUnfavorite={isFav === "unFavorite"} 
        on:click={() => dispatch('toggle-class') }>{isFav}</button>
        <button class="button" on:click={() => dispatch("show-detail")}>Show details</button>
        <button class="delete" on:click={() => deleteMeet (id)}>x</button>
    </footer>
</article>

<style>
    .active {
        background-color: rgba(0, 0, 0, .5)
    }
    article {
        position: relative;
        background-color: white;
        box-shadow: 0px 2px 8px rgba(0, 0, 0, 0.26);
        border-radius: 10px;
        width: 90%;
        margin: 1rem;
        }
        article header {
            display: flex;
            justify-content: space-between;
        }
    header, .content, footer {
        padding: 1rem;
        }
    .image {
        width: 100%;
        object-fit: cover;
        }
    img {
        width: 250px;
        height: 250px;
        display: block;
        margin: auto
    }
    .favorito {
        background-color: #cf0056;
        color: aliceblue;
        padding: 8px;
        opacity: 70%;
        margin-top: 10px;
    }
    h1 {
        font-size: 1.25rem;
         margin: 0.5rem, 0;
    }
    h1 {
        font-size: 1.25rem;
        margin: 0.5rem 0;
        font-family: "Roboto Slab", sans-serif;
    }

    h2 {
        font-size: 1rem;
        color: #808080;
        margin: 0.5rem 0;
    }
    .bgUnfavorite {
        border: 2px solid #cf0056;
        color: #cf0056;
        padding: 8px;
        border-radius: 5px;
        text-align: center;
        margin-right: 10px;
    }
    .bgFavorite {
         border: 2px solid #01a129;
        color: #01a129;
        padding: 8px;
        border-radius: 5px;
        text-align: center;
        margin-right: 10px;
    }
    .button {
        border: 1px solid #cf0056;
        padding: 8px;
        border-radius: 5px;
        color: white;
        background-color: #cf0056;
        text-align: center;
        margin-right: 10px;

    }

    p {
        font-size: 1.25rem;
        font-weight: bolder;
        margin: 0;
    }

    div {
        text-align: center;
    }
    .delete {
        position: absolute;
        background-color: transparent;
        border: none;
        top: 1px;
        right: 10px;
        font-weight: bolder;
        opacity: 80%;
        color: #cf0056;
    }
</style>