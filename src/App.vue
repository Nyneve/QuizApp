<template>
  <div id="app">
    <div class="box" v-if="frage_nummer < 7">
      ( Frage {{ frage_nummer + 1 }} von {{ question.length }} )<br>
      <h2>Was bedeutet {{ question[frage_nummer] }}?</h2>
      <div class="inhalt">
        <button class="answers" @click="frage_nummer++, sortier(), clicked(0)">{{ answer[frage_nummer][0] }}</button>
        <button class="answers" @click="frage_nummer++, sortier(), clicked(1)">{{ answer[frage_nummer][1] }}</button>
        <button class="answers" @click="frage_nummer++, sortier(), clicked(2)">{{ answer[frage_nummer][2] }}</button>
        <button class="answers" @click="frage_nummer++, sortier(), clicked(3)">{{ answer[frage_nummer][3] }}</button>
      </div>
      
    </div>
    <div class="box" v-else>
      <div class="inhalt">
        <h2>Du hast {{ resultat }} von {{ question.length }} Fragen richtig.</h2><br><br>
        <button class="again" @click="frage_nummer = 0, resultat = 0">Erneut versuchen</button>
      </div>
    </div>
    <center>
    </center>
  </div>
</template>

<script>
export default {
  name: 'App',

  data: () => ({
    question: ["USV", "ROM", "PIN", "POE", "PXE", "DNS", "URL"],
    answer: [
      ["Unterbrechungsfreie Stromversorgung", "Universelle Steckdose", "Universal-Steckdosen-Verbindung", "US-Version"],
      ["Read only memory", "Ready on memory", "Read on memory", "Return on Memory"],
      ["Personal Identification Number", "Private Identification Number", "Personal IQ Number", "Private Idenfication Name"],
      ["Power over Ethernet", "Presentation over Ethernet", "Power on Ethernet", "Presentation on Ethernet"],
      ["Preboot Execution Enviroment", "Pastboot Enviroment", "Preexecutable Envviroment", "Pastexecution Exercise"],
      ["Domain Name System", "Domain Number System", "Domain Name Slogan", "Domain Number Server"],
      ["Uniform Resource Locator", "Universal Resouce Locator", "Uniform Resource Loader", "Universal Resource Loader"]
    ],
    antwort_nummer: 0,
    frage_nummer: 0,
    resultat: 0,
    richtig: 0,
    durchlauf: 0,

    sortier: function () {
      let nummer = [0, 1, 2, 3];
      nummer = nummer.sort(() => Math.random() - 0.5)
      var nummer0 = nummer[0];
      var nummer1 = nummer[1];
      var nummer2 = nummer[2];
      var nummer3 = nummer[3];
      return [nummer0, nummer1, nummer2, nummer3];
    }
  }),

  computed: {
    korrekt: function () {
      return this.answer[this.frage_nummer][0];
    }
  },

  methods: {
    clicked(val) {
      var click = val;
      if (click == this.richtig) {
        this.resultat++;
      }
      return this.resultat;
    },

    loesung(val) {
      var loes = val;
      if (loes == 1) {
        document.getElementById("answers").style.border = "1px solid #ff0000";
      }
      else if (loes == 2) {
        document.getElementById("answers").style.border = "1px solid #ffffff";
      }
    },

    mounted() {
      this.sortier();
    }
  }
}
</script>

<style>@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500&display=swap');
@import 'assets/style.css';</style>