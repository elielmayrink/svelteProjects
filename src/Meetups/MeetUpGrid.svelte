<script>
    import MeetUpsItem from './MeetUpsItem.svelte';
    export let meetUps;
    export let modalState;
    export let deleteEvent;
    export let exit;
</script>	
    
    <section on:click={exit} id="meetup" >
		{#each meetUps as meetUp}
			<MeetUpsItem
			deleteMeet={() => deleteEvent(meetUp.id)} 
			active={modalState}
			id={meetUp.id}
			email={meetUp.contactEmail}
			address={meetUp.address}
			title={meetUp.title}
			subtitle={meetUp.subtitle}
			imageUrl={meetUp.imageUrl}
			descriptions={meetUp.description}
			favorite={meetUp.fav}
			isFav={meetUp.fav ? "unFavorite" : "Favorite"}
			detail={meetUp.detail}
			on:toggle-class={() => {
				if(meetUp.id === meetUp.id){
					meetUp.fav = !meetUp.fav
				}
				}}	
			/>
		{/each}
	</section>
<style>
    #meetup {
		margin: 2rem;
        display: grid;
        grid-template-columns: 1fr 1fr;
	}    
</style>