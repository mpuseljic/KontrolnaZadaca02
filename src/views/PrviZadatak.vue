<template>
	<v-container fill-height fluid class="background">
		<v-row>
			<v-col cols="12">
				<v-card class="pa-3" outlined width="600px">
					<v-card-title>Dodaj studenta</v-card-title>
					<v-card-text>
						<v-form v-model="valid">
							<v-text-field
								v-model="ime"
								dense
								label="Ime"
								clearble
								:rules="[rules.required]"
								type="text"
								outlined></v-text-field>
							<v-text-field
								v-model="prezime"
								dense
								label="Prezime"
								clearble
								:rules="[rules.required]"
								type="text"
								outlined></v-text-field>
							<v-text-field
								v-model="brojDolazaka"
								dense
								label="Broj dolazaka (maksimalno 15)"
								clearble
								:rules="[rules.required, rules.min]"
								type="text"
							
								outlined></v-text-field>
							<v-text-field
								v-model="prviKolokvij"
								dense
								label="Rezultati prvog kolokvija(maksimalno 40 bodova)"
								clearble
								:rules="[rules.required]"
								type="text"
								
								outlined></v-text-field>
							<v-text-field
								v-model="drugiKolokvij"
								dense
								label="Rezultati drugog kolokvija(maksimalno 40 bodova)"
								clearble
								:rules="[rules.required]"
								type="text"
								
								outlined></v-text-field>
							<v-text-field
								v-model="kontinuiranoPracenje"
								dense
								label="Kontinuirano pracenje(maksimalno 20 bodova)"
								clearble
								:rules="[rules.required, rules.minPracenje]"
								type="text"
			
								outlined></v-text-field>
						</v-form>
					</v-card-text>
					<v-card-actions>
						<v-btn
							color="black"
							class="white--text"
							elevation="0"
							@click="obrisiSveUnesenePodatke">
							BRISI PODATKE
						</v-btn>

						<v-btn
							class="btn-right-margin"
							@click="ocistiFormu"
							color="red darken-3"
							outlined>
							CLEAR
						</v-btn>
						<v-btn
							:disabled="isButtonDisabled"
							outlined
							@click="dodajStudenta"
							>
							OK
						</v-btn>
						<v-spacer></v-spacer>
					</v-card-actions>
				</v-card>
			</v-col>
		</v-row>
	</v-container>
</template>

<script>
import store from '@/store'

export default {
	name: "prvi-zadatak",
	data() {
		return {
			ime: null,
			prezime: null,
			brojDolazaka: null,
			prviKolokvij: null,
			drugiKolokvij: null,
			kontinuiranoPracenje: null,
			rules: {
				required: (value) => !!value || "Required.",
				min:(value)=>{
					if (value<11){
						return "Not valid."

					}
			
				},
				minPracenje:(value)=>{
					if(value<5)
						return "Not valid."
				},

			},
		};
	},
	watch: {
		valid: function (newVal) {
			if (newVal != true) {
				this.isButtonDisabled = true;
			} else {
				this.isButtonDisabled = false;
			}
		},
	},
	computed:{
		isButtonDisabled(){
			return!(this.ime && this.prezime && this.prviKolokvij && this.drugiKolokvij&& this.kontinuiranoPracenje)
		}
		
	},
	methods: {
		ocistiFormu() {
			this.ime = null;
			this.prezime = null;
			this.brojDolazaka = null;
			this.prviKolokvij = null;
			this.drugiKolokvij = null;
			this.kontinuiranoPracenje = null;
		},
		dodajStudenta() {
			let noviStudent = {
				ime: this.ime,
				prezime: this.prezime,
				brojDolazaka: this.brojDolazaka,
				prviKolokvij: this.prviKolokvij,
				drugiKolokvij: this.drugiKolokvij,
				kontinuiranoPracenje: this.kontinuiranoPracenje

			};
			//ovo ne diraj
			let studenti = JSON.parse(localStorage.getItem("studenti"));
			if (!studenti) {
				studenti = [];
			}
			studenti.push(noviStudent);
			localStorage.setItem("studenti", JSON.stringify(studenti));
			this.ocistiFormu();
		},
		obrisiSveUnesenePodatke() {
			localStorage.clear();
		},

	
	},
};
</script>

<style>
.card-actions {
	display: flex;
	align-items: center;
	justify-content: flex-end;
}

</style>