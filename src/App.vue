<template>
	<div>
		<div id="slogan" class="text-center">
			<h1>SeparaTimes</h1>
			<br/>
			<h6 class="text-secondary">Separa os times da pelega de terça</h6>
		</div>
		<div id="main">
			<div class="container">
        <h5>Confirmados <span class="badge badge-info">{{ jogadores.length }}</span></h5>
				<div class="card">
					<div class="card-body">
						<ul class="list-group">
							<li class="list-group-item" v-for="jogador in jogadores" v-bind:key="jogador">
                <div class="row">
								<div class="col-md">
								{{ jogador }}
                </div>
											<div class="col-md text-right">
												<button class="btn btn-info btn-sm" v-on:click="deleteJogador(jogador)"><span class="fa fa-trash"></span></button>
											</div>
										</div>
							</li>
						</ul>
            <br/>
								<div class="input-group">
									<input class="form-control" type="text" v-model="jogador" v-on:keyup.enter="addJogador(jogador)" placeholder="Adicionar confirmado"/>
									<div class="input-group-append">
										<button class="btn btn-info" v-on:click="addJogador(jogador)"><span class="fa fa-plus"></span></button>
									</div>
								</div>
                <br/>
                <div class="btn-toolbar" role="toolbar" aria-label="Toolbar with button groups">
                <div class="btn-group mr-2" role="group" >
										<button class="btn btn-info" v-on:click="gerarTimes()">Gerar Times</button>              
								</div>
                <div class="btn-group mr-2" role="group" >  
                    <button class="btn btn-info" v-on:click="limparTimes()">LimparTimes</button>             
								</div>
                </div>
					</div> 								
				</div>
        <br/>
				<div class="row">
					<div class="col-md">
						<h5>Time Azul <span class="badge badge-primary">{{ timeAzul.length }}</span></h5>
						<div class="card">
							<div class="card-body">
								<ul class="list-group">
									<li class="list-group-item" v-for="azul in timeAzul" v-bind:key="azul">
										<div class="row">
											<div class="col-md">
												{{ azul }}
											</div>
											<div class="col-md text-right">
												<button class="btn btn-info" v-on:click="deleteTimeAzul(azul)"><span class="fa fa-trash"></span></button>
											</div>
										</div>
									</li>
								</ul>								
							</div>
						</div>
					</div>
					<div class="col-md">
						<h5>Time Vermelho <span class="badge badge-danger">{{ timeVermelho.length }}</span></h5>
						<div class="card">
							<div class="card-body">
								<ul class="list-group">
									<li class="list-group-item" v-for="vermelho in timeVermelho" v-bind:key="vermelho">
										<div class="row">
											<div class="col-md">
												{{ vermelho }}
											</div>
											<div class="col-md text-right">
												<button class="btn btn-info" v-on:click="deleteTimeVermelho(vermelho)"><span class="fa fa-trash"></span></button>
											</div>
										</div>
									</li>
								</ul>								
							</div>
						</div>
					</div>
				</div>
				<br/>				
			</div>
		</div>
	</div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";
export default {
	name: "app",
	data: function () {
		return {
      meio: 0,
      timeAzul: [],
      timeVermelho: [],
      jogadores: [],
      jogadoresSorteados: []
		};
	},
	methods: {
    addJogador(jogador) {
			this.jogadores.push(jogador);
			this.jogador = "";
    },
    deleteTimeAzul(azul) {
			this.timeAzul.splice(this.timeAzul.indexOf(azul), 1);
    },
    deleteTimeVermelho(vermelho) {
			this.timeVermelho.splice(this.timeVermelho.indexOf(vermelho), 1);
    },
    deleteJogador(jogador) {
			this.jogadores.splice(this.jogadores.indexOf(jogador), 1);
    },    
    limparTimes() {
      this.timeVermelho = [];
      this.timeAzul = [];
    },
    gerarTimes() {
      this.limparTimes();
      this.jogadoresSorteados = this.jogadores.slice();
      this.jogadoresSorteados = this.jogadoresSorteados.sort();
      this.meio = this.jogadoresSorteados.length / 2;

      while (this.meio >= 1) {
        this.timeAzul.push(this.jogadoresSorteados.shift());
        this.meio = this.meio - 1;
      }

      this.timeVermelho = this.jogadoresSorteados;

      this.meio = 0;
    }	
	}
};
</script>

<style>
#slogan {
	margin-top: 30px;
	margin-bottom: 30px;
}
#main {
	background-color: #F1F1F1;
	padding-top: 30px;
	padding-bottom: 30px;
}
</style>