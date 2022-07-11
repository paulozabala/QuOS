<template>
	<v-container >
		<v-row justify="center">
			<v-card
				class="pa-8 mt-16"
			>
				<form >
					<v-text-field
						v-model="user"
						:error-messages="userErrors"
						:counter="8"
						label="Usuario"
						required
						@input="$v.user.$touch()"
						@blur="$v.user.$touch()"
					></v-text-field>
					<v-text-field
						v-model="password"
						:error-messages="passErrors"
						label="Password"
						required
						@input="$v.password.$touch()"
						@blur="$v.password.$touch()"
					></v-text-field>
					<v-card flat class="d-flex justify-center mt-4" >
					<v-btn 
						class=""
						@click="submit"
						width="120px"
					>
						Ingresar
					</v-btn>
					<v-btn
						class="ml-8"
						@click="Register" 
						width="120px"
					>Registrarse
					</v-btn>
					</v-card>
				</form>
			</v-card>
		</v-row>
	</v-container>
</template>
<script>

import { validationMixin } from 'vuelidate'
import { required, maxLength } from 'vuelidate/lib/validators'

export default {
	name: 'Login_R',

	mixins: [validationMixin],

	validations: {
		user: { required, maxLength: maxLength(8) },
		password: { required, maxLength: maxLength(8) },
	},

	data: () => ({
		user: '',
		password :''
	}),

	computed: {
		userErrors () {
			const errors = []
			if (!this.$v.user.$dirty) return errors
			!this.$v.user.maxLength && errors.push('Usuario debe tener máximo 8 caracteres')
			!this.$v.user.required && errors.push('Este campo es obligatorio')
			return errors
		},
		passErrors () {
			const errors = []
			if (!this.$v.password.$dirty) return errors
			!this.$v.password.maxLength && errors.push('debe contener 8 caracteres como mínimo')
			!this.$v.password.required && errors.push('Este campo es obligatorio')
			return errors
			},
		},

	methods: {
		submit () {
			this.$v.$touch()
		},
		clear () {
			this.$v.$reset()
			this.name = ''
			this.email = ''
			this.select = null
			this.checkbox = false
		}
	}
}


</script>
