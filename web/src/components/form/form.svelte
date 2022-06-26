<script>
    import {createObjectCsvWriter} from '../../../../node_modules/csv-writer/src/index.ts'

    export let path 
    const csvWriter = createObjectCsvWriter({
        path: path
    });

	let wolof;
	let francais;
    let anglais;
	let errors = {
	  wolof: "",
	  francais: "",
      anglais: ""
	};

    const records = [
    {Wolof: wolof ,  Français: francais, Anglais: anglais},
];

	const onSubmit = () => {
	  errors.wolof = "";
	  if (wolof === undefined || wolof.trim() === "") {
	    errors.wolof = "wolof is required";
	    return;
	  }
	  if (francais === undefined || francais.trim() === "") {
	    errors.francais = "francais is required";
	    return;
	  }
      if (anglais === undefined || anglais.trim() === "") {
	    errors.anglais = "anglais is required";
	    return;
	  }
      csvWriter.writeRecords(records)       
        .then(() => {
            console.log('...Done');
        });
	};

</script>

<div class="p-20">
  <form on:submit|preventDefault={onSubmit}>
    <label for="wolof" class="block text-sm text-gray-600">wolof</label>
    <input id="wolof" type="text" placeholder="wolof" class="block px-1 py-2 mt-2 border-2 border-gray-100 text-gray-800" bind:value={wolof} />
    {#if errors.wolof}
    	<small class="block mt-1 mb-4 text-xs italic text-red-700 capitalize-first">{errors.wolof}</small>
    {/if}
    
    <label for="francais" class="block text-sm text-gray-600 mt-4">francais</label>
    <input id="francais" type="francais" bind:value={francais} placeholder="francais" class="block px-1 py-2 mt-2 border-2 border-gray-100 text-gray-800" />

    <label for="anglais" class="block text-sm text-gray-600 mt-4">anglais</label>
    <input id="anglais" type="anglais" bind:value={anglais} placeholder="anglais" class="block px-1 py-2 mt-2 border-2 border-gray-100 text-gray-800" />

    <button type="submit" class="p-2 bg-blue-500 text-white mt-4 px-6">
      Enregistrer
    </button>
  </form>
</div>