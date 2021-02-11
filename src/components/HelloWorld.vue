<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-5" cols="12">
        <v-row justify="center">
          <div v-for="option in options" :key="option.item">
            <v-avatar
              class="ma-2"
              color="primary"
              size="70"
              @click="play(option.item)"
              >{{ option.item }}</v-avatar
            >
          </div>
        </v-row>
        <div class="mt-10">
          Jogador <v-chip class="ml-3 mr-3">{{ placar.jogador }}</v-chip> X
          <v-chip class="mr-3 ml-3">{{ placar.computador }}</v-chip> Computador
        </div>
        <div class="mt-10">
          {{ message }}
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    options: [
      { item: "Pedra" },
      { item: "Papel" },
      { item: "Tesoura" },
      { item: "Lagarto" },
      { item: "Spock" },
    ],
    playerOption: "",
    placar: {
      jogador: 0,
      computador: 0,
    },
    message: "",
  }),
  methods: {
    play(jogador) {
      var escolha = Math.round(Math.random() * 4);
      var computador = this.options[escolha].item;
      this.getVencedor(jogador, computador);
    },

    vencedor(vencedor, message){
      if(vencedor = 'jogador'){
        this.placar.jogador +=1
        this.message = message + '. Jogador Vence'
      }else if(vencedor == 'computador'){
        this.placar.computador +=1
        this.message = message + '. Computador Vence'
      }else{
        this.message = "Empate..."
      }
    },

    getVencedor(jogador, computador) {
      if (jogador == "Pedra") {
        if (computador == "Lagarto") {
          this.vencedor('jogador', 'Pedra Esmaga Lagarto')
        } else if (computador == "Tesoura") {
          this.vencedor('jogador', 'Pedra Amassa Tesoura')
        }
      } else if (jogador == "Papel") {
        if (computador == "Pedra") {
          this.vencedor('jogador', 'Papel cobre pedra')
        }
        if (computador == "Spock") {
          this.vencedor('jogador', 'Papel refuta Spock')
        }
      } else if (jogador == "Tesoura") {
        if (computador == "Papel") {
          this.vencedor('jogador', 'Tesoura corta papel')
        }
        if (computador == "Lagarto") {
          this.vencedor('jogador', 'Tesoura decapita lagarto')
        }
      } else if (jogador == "Lagarto") {
        if (computador == "Spock") {
          this.vencedor('jogador', 'Lagarto envenena Spock')
        }
        if (computador == "Papel") {
          this.vencedor('jogador', 'Lagarto come papel')
        }
      } else if (jogador == "Spock") {
        if (computador == "Tesoura") {
          this.vencedor('jogador', 'Spock derrete tesoura')
        }
        if (computador == "Vaporiza") {
          this.vencedor('jogador', 'Spock vaporiza pedra')
        }
      }
    },
  },
};
</script>
