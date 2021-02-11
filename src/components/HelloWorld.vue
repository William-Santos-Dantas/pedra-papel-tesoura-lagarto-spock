<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-5" cols="12">
        <v-row justify="center">
          <div v-for="option in options" :key="option.item">
            <v-avatar
              class="ma-2"
              :color="option.color"
              size="70"
              @click="play(option.item)"
              >{{ option.item }}</v-avatar
            >
          </div>
        </v-row>
        <div class="mt-10">
          <v-avatar class="ma-2" :color="computerOption.color" size="70">{{
            computerOption.item
          }}</v-avatar>
        </div>
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
      { item: "Pedra", color: "red lighten-2" },
      { item: "Papel", color: "purple lighten-2" },
      { item: "Tesoura", color: "indigo darken-1" },
      { item: "Lagarto", color: "teal darken-4" },
      { item: "Spock", color: "green lighten-1" },
    ],
    playerOption: "",
    computerOption: {
      item: '', color: ''
    },
    placar: {
      jogador: 0,
      computador: 0,
    },
    message: "",
  }),
  methods: {
    async computadoroption() {
      for (var i = 0; i < 15; i++) {
        var escolha = Math.round(Math.random() * 4);
        this.computerOption = this.options[escolha];
        await this.sleep(100);
      }
      return true;
    },

    sleep(ms) {
      return new Promise((resolve) => setTimeout(resolve, ms));
    },

    play(jogador) {
      this.computadoroption().then((response) => {
        this.getVencedor(jogador, this.computerOption.item);
      });
    },

    vencedor(vencedor, message) {
      if (vencedor == "jogador") {
        this.placar.jogador += 1;
        this.message = message + ". Jogador Vence";
      } else if (vencedor == "computador") {
        this.placar.computador += 1;
        this.message = message + ". Computador Vence";
      } else if (vencedor == "empate") {
        this.message = "Empate...";
      }
    },

    pedra(computador) {
      if (computador == "Lagarto") {
        this.vencedor("jogador", "Pedra Esmaga Lagarto");
      } else if (computador == "Tesoura") {
        this.vencedor("jogador", "Pedra Amassa Tesoura");
      } else if (computador == "Papel") {
        this.vencedor("computador", "Papel cobre pedra");
      } else if (computador == "Spock") {
        this.vencedor("computador", "Spock vaporiza pedra");
      }
    },

    papel(computador) {
      if (computador == "Pedra") {
        this.vencedor("jogador", "Papel cobre pedra");
      } else if (computador == "Spock") {
        this.vencedor("jogador", "Papel refuta Spock");
      } else if (computador == "Tesoura") {
        this.vencedor("computador", "Tesoura corta papel");
      } else if (computador == "Lagarto") {
        this.vencedor("computador", "Lagarto come papel");
      }
    },

    tesoura(computador) {
      if (computador == "Papel") {
        this.vencedor("jogador", "Tesoura corta papel");
      } else if (computador == "Lagarto") {
        this.vencedor("jogador", "Tesoura decapita lagarto");
      } else if (computador == "Spock") {
        this.vencedor("computador", "Spock derrete tesoura");
      } else if (computador == "Pedra") {
        this.vencedor("computador", "Pedra Amassa Tesoura");
      }
    },

    lagarto(computador) {
      if (computador == "Spock") {
        this.vencedor("jogador", "Lagarto envenena Spock");
      } else if (computador == "Papel") {
        this.vencedor("jogador", "Lagarto come papel");
      } else if (computador == "Pedra") {
        this.vencedor("computador", "Pedra esmaga lagarto");
      } else if (computador == "Tesoura") {
        this.vencedor("computador", "Tesoura decapita lagarto");
      }
    },
    spock(computador) {
      if (computador == "Tesoura") {
        this.vencedor("jogador", "Spock derrete tesoura");
      } else if (computador == "Pedra") {
        this.vencedor("jogador", "Spock vaporiza pedra");
      } else if (computador == "Lagarto") {
        this.vencedor("computador", "Lagarto envenena Spock");
      } else if (computador == "Papel") {
        this.vencedor("computador", "Papel refuta Spock");
      }
    },

    getVencedor(jogador, computador) {
      if (jogador == computador) {
        this.vencedor("empate", "");
      } else {
        if (jogador == "Pedra") {
          this.pedra(computador);
        } else if (jogador == "Papel") {
          this.papel(computador);
        } else if (jogador == "Tesoura") {
          this.tesoura(computador);
        } else if (jogador == "Lagarto") {
          this.lagarto(computador);
        } else if (jogador == "Spock") {
          this.spock(computador);
        }
      }
    },
  },
};
</script>
