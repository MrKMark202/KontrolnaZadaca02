<template>
	<v-container fill-height fluid class="background">
		<v-row>
			<v-col cols="12">
				<v-card class="pa-3" outlined width="600px">
					<v-card-title>Dodaj studenta</v-card-title>
					
					<v-text-field
					label="Ime"
					type="text"
					v-model="ime"
					:rules="[rules.required]"
					>
						<template v-slot:label></template>
					</v-text-field>

					<v-text-field
					label="Prezime"
					type="text"
					v-model="prezime"
					:rules="[rules.required]"
					>
						<template v-slot:label></template>
					</v-text-field>

					<v-text-field
					label="Broj dolazaka (max 15)"
					type="text"
					v-model="dolazak"
					:rules="[rules.required]"
					>
						<template v-slot:label></template>
					</v-text-field>

					<v-text-field
					label="Rezultat prvog kolokvija (max 40)"
					type="text"
					v-model="prviKol"
					:rules="[rules.required]"
					>
						<template v-slot:label></template>
					</v-text-field>

					<v-text-field
					label="Rezultat drugog kolokvija (max 40)"
					type="text"
					v-model="drugiKol"
					:rules="[rules.required]"
					>
					<template v-slot:label></template>
					</v-text-field>

					<v-text-field
					label="Kontinuirano praćenje (max 20)"
					type="text"
					v-model="konPracenje"
					:rules="[rules.required]"
					>
						<template v-slot:label></template>
					</v-text-field>

					<div class="grid">

						<v-card-actions>
							<v-btn
								color="black"
								class="white--text"
								elevation="0"
								@click="obrisiSveUnesenePodatke">
								BRISI PODATKE
							</v-btn>
						

							<v-btn style="color: red; margin-left: 250px" @click="ocistiFormu()">Ocisti</v-btn>
							<v-btn
								style="margin-left: 20px"
								type="button"
								:disabled="form"
								:loading="isLoading"
								depressed
								@click="dodajStudenta()"
							>OK</v-btn>
						</v-card-actions>
					</div>
				</v-card>
			</v-col>
		</v-row>
	</v-container>
</template>

<script>
export default {
	name: "prvi-zadatak",
	data() {
		return {
			ime: null,
			prezime: null,
			dolazak: null,
			prviKol: null,
			drugiKol: null,
			konPracenje: null,
			form: false,
      		isLoading: false,
			agreement: false,
      		valid: true,
			rules: {
				required: v => !!v || 'This field is required'
			}
		};
	},
	watch: {},
	methods: {
		ocistiFormu() {
			this.ime = null,
			this.prezime = null,
			this.dolazak = null,
			this.prviKol = null,
			this.drugiKol = null,
			this.konPracenje = null
		},

		dodajStudenta() {
			let noviStudent = {
				Ime: this.ime,
				Prezime: this.prezime,
				Dolazak: this.dolazak,
				PrviKol: this.prviKol,
				DrugiKol: this.drugiKol,
				KonPracenje: this.konPracenje

			};
			//ovo ne diraj
			let studenti = JSON.parse(localStorage.getItem("studenti"));
			if (!studenti) {
				studenti = [];
			}
			studenti.push(noviStudent);
			localStorage.setItem("studenti", JSON.stringify(studenti));

			this.obrisiSveUnesenePodatke();
		},
		obrisiSveUnesenePodatke() {
			localStorage.clear();
		},
	},
};
</script>

<style>

.grid
{
	display: grid;
    grid-template-columns: auto auto auto;
	padding: 20px;
}

.grid-item
{

}

.ocisti
{
	color: red;
}

</style>
