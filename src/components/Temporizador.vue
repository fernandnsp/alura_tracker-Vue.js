<template>
	<div class="is-flex is-align-items-center is-justify-content-space-between">
		<Cronometro :tempoEmSegundos="tempoEmSegundos"/>
		
		<Botao @evento="iniciar" icone="fas fa-play" texto="Play" :disabled="cronometroRodando"/>
		<Botao @evento="finalizar" icone="fas fa-stop" texto="Stop" :disabled="!cronometroRodando"/>
	</div>
</template>

<script lang="ts">
	import { defineComponent } from 'vue'
	import Cronometro from './Cronometro.vue'
	import Botao from './Botao.vue'

	export default defineComponent({
		name: 'Temporizador',
		emits: ['temporizadorFinalizado'],
		components: {
			Cronometro,
			Botao
		},
		data(){
			return{
				tempoEmSegundos: 0,
				cronometro: 0,
				cronometroRodando: false,
			}
		},
		methods: {
			iniciar(){
				this.cronometroRodando = true
				this.cronometro = setInterval(() => {
					this.tempoEmSegundos += 1
				}, 1000)
			},
			finalizar(){
				this.cronometroRodando = false
				clearInterval(this.cronometro)
				this.$emit('temporizadorFinalizado', this.tempoEmSegundos)
				this.tempoEmSegundos = 0
			}
		}
	})
</script>