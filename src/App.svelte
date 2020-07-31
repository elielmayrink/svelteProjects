<script>
	import Header from './UI/Header.svelte';
	import MeetUpgrid from './Meetups/MeetUpGrid.svelte';
	let title = "";
	let subtitle = "";
	let imageUrl = "";
	let description = "";
	let address = "";
	let contactEmail = "";
	let modalState = "standBy";
	let meetUpState = "all";

	let meetUps = [
		{
			id: "m1",
			title: "Tudo sobre investimento na bolsa",
			subtitle: "Ações ou Fundos imobiliarios?",
			description: "Tudo que você precisa saber sobre investimento na bolsa de valores, fundos imobiliarios ou ações",
			imageUrl: "https://images.pexels.com/photos/128867/coins-currency-investment-insurance-128867.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
			address: "rua 15 de novembro 2550 Joinville Vila nova",
			contactEmail: "tudosobreinvest@ibovespa.com.br",
			fav: false,
			detail: false
		},
		{
			id: "m2",
			title: "A verdade sobre o Papai noel",
			subtitle: "Ele existe?",
			description: "Todas suas duvidas sobre o bom velhinho serão sanadas... duvidas nunca mais",
			imageUrl: "https://images.pexels.com/photos/133640/pexels-photo-133640.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940",
			address: "rua honorio benevenutti 144",
			contactEmail: "renas@polonorte.com.br",
			fav: false,
			detail: false
		},
		{
			id: "m3",
			title: "Pé grande",
			subtitle: "Ele esta entre nós",
			description: "Dos mesmo dismitificadores de papai noel vc tera a certeza que o grande monstro das montanhas existe ",
			imageUrl: "https://images.pexels.com/photos/4075/nature-walking-animal-strong.jpg?auto=compress&cs=tinysrgb&dpr=1&w=500",
			address: "rua pé da montanha 1500",
			contactEmail: "naoexiste@sapatosparamim.com.br",
			fav: false,
			detail: false
		}
	];
	function toggleStateModal() {
		modalState = "active"
	}
	function addMeetUp () {
		if(
			title.trim().length === 0 ||
			subtitle.trim().length === 0 ||
			imageUrl.trim().length === 0 ||
			description.trim().length === 0 ||
			address.trim().length === 0 ||
			contactEmail.trim().length === 0
		) {
			alert("PLEASE INSERT THE DATAS IN THE INPUTS!!!!")
			return
		}
		meetUps = [
		...meetUps, 
			{
				id: Math.random(),
				title: title,
				subtitle: subtitle,
				description: description,
				imageUrl: imageUrl,
				address: address,
				contactEmail: contactEmail,
				fav: false,
				detail: false
			}
		];
		modalState = "standby";
	};
	function exit () {
		modalState = "standBy"
	}
	function deleteEvent (id) {
		meetUps = meetUps.filter(m => m.id !== id);
	}
</script>

<Header />
<main class:active={modalState === "active"}>
	<div>
		<MeetUpgrid
			exit={exit}
			modalState={modalState} 
			meetUps={meetUps}
			deleteEvent={deleteEvent} />

		<button on:click={toggleStateModal} class="add">Add meetUp</button>
	</div>
	{#if modalState === "active"}
		<form on:submit|preventDefault={addMeetUp} class="modal">
		<h1>Please enter yours meetUps</h1>
		<input type="text" placeholder="Title" bind:value={title}>
		<input type="text" placeholder="Subtitle" bind:value={subtitle}>
		<input type="text" placeholder="ImageUrl" bind:value={imageUrl}>
		<input type="text" placeholder="address" bind:value={address}>
		<input type="email" placeholder="contactEmail" bind:value={contactEmail}>
		<textarea rows="10" bind:value={description}></textarea>
		<button type="submit" >Add Meetup</button>
		</form>
	{/if}
</main>
<style>
	main {
		margin: 5rem;
	}
	.active {
		background-color: rgba(0, 0, 0, .5);
		z-index: inherit;
		margin: 0;
		width: 100%;
		height: auto;
		overflow-y: hidden;
	}
	.add {
		padding: 10px;
		border-radius: 10px;
		background-color: #cf0056;
		color: white;
		opacity: .8;
		position: fixed;
		bottom: 0;
		right: 0;
	}
	 .modal {
        width: 550px;
        background-color: white;
        margin: auto;
        padding: 8px;
        text-align: center;
        border-radius: 10px;
        box-shadow: 1px 2px 6px #ccc;
        position: fixed;
        top: 100px;
        left: 400px;
    }
    input {
        display: block;
        width: 90%;
        margin: auto;
        margin-bottom: 5px;
        background-color: azure;
    }
    textarea {
        width: 90%;
        height: 100px;
        overflow-y: hidden;
    }
    button {
        background-color: #ccc;
        padding: 10px;
        border-radius: 8px;
    }
</style>



