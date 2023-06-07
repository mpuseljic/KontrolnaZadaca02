<template>
	<v-container fill-height fluid class="background">
		<v-row>
			<v-col cols="12">
				<v-card class="pa-3" outlined width="600px">
					<v-card-title>Dodaj studenta</v-card-title>
					<v-card-text>
						<v-form v-model="valid">
							<v-text-field
								v-model="firstName"
								dense
								label="Ime"
								clearble
								:rules="[rules.required]"
								type="text"
								outlined></v-text-field>
							<v-text-field
								v-model="lastName"
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
								:rules="[rules.required]"
								type="text"
							
								outlined></v-text-field>
							<v-text-field
								v-model="rezultatiPrvogKolokvija"
								dense
								label="Rezultati prvog kolokvija(maksimalno 40 bodova)"
								clearble
								:rules="[rules.required]"
								type="text"
								
								outlined></v-text-field>
							<v-text-field
								v-model="rezultatiDrugogKolokvija"
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
								:rules="[rules.required]"
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
export default {
	name: "prvi-zadatak",
	data() {
		return {
			firstName: null,
			lastName: null,
			brojDolazaka: null,
			rezultatiPrvogKolokvija: null,
			rezultatiDrugogKolokvija: null,
			kontinuiranoPracenje: null,
			isButtonDisabled: false,
			rules: {
				required: (value) => !!value || "Required.",
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
	methods: {
		ocistiFormu() {
			this.firstName = null;
			this.lastName = null;
			this.brojDolazaka = null;
			this.rezultatiPrvogKolokvija = null;
			this.rezultatiDrugogKolokvija = null;
			this.kontinuiranoPracenje = null;
		},
		dodajStudenta() {
			let noviStudent = {
				//Dodaj propertyje
			};
			//ovo ne diraj
			let studenti = JSON.parse(localStorage.getItem("studenti"));
			if (!studenti) {
				studenti = [];
			}
			studenti.push(noviStudent);
			localStorage.setItem("studenti", JSON.stringify(studenti));
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