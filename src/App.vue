<template>
  <div id="app">
    <textarea v-model="input" cols="100" rows="30"></textarea>
    <br />
    <br />
    <br />
    <div v-html="highlightedContent"></div>
  </div>
</template>

<script>
  export default {
    name: 'app',
    data() {
      return {
        input: "[{\"Word\":\"immune response\"},{\"Word\":\"homeostasis\"},{\"Word\":\"IL\"},{\"Word\":\"IL-1\"},{\"Word\":\"inflammation\"},{\"Word\":\"inflammatory\"},{\"Word\":\"ion\"},{\"Word\":\"iron\"},{\"Word\":\"irradiation\"},{\"Word\":\"response\"},{\"Word\":\"resting\"},{\"Word\":\"L\"},{\"Word\":\"lung\"},{\"Word\":\"pneumonitis\"},{\"Word\":\"microenvironment\"},{\"Word\":\"monocyte\"},{\"Word\":\"syngeneic\"},{\"Word\":\"pons\"},{\"Word\":\"port\"},{\"Word\":\"pulmonary\"},{\"Word\":\"radiation\"},{\"Word\":\"receptor\"},{\"Word\":\"recipient\"},{\"Word\":\"sign\"},{\"Word\":\"anal\"},{\"Word\":\"duct\"},{\"Word\":\"macrophage\"},{\"Word\":\"attenuated\"},{\"Word\":\"bone marrow\"},{\"Word\":\"CD20\"},{\"Word\":\"cell\"},{\"Word\":\"chimeric\"},{\"Word\":\"cytokine\"},{\"Word\":\"donor\"},{\"Word\":\"fibrosis\"},{\"Word\":\"observation\"},{\"Word\":\"gene\"},{\"Word\":\"thoracic\"},{\"Word\":\"tissue\"},{\"Word\":\"wound\"}]",
        query: "",
        content: "Lung exposure to radiation induces an injury response that includes the release of cytokines and chemotactic mediators; these signals recruit immune cells to execute inflammatory and wound-healing processes. However, radiation alters the pulmonary microenvironment, dysregulating the immune responses and preventing a return to homeostasis. Importantly, dysregulation is observed as a chronic inflammation, which can progress into pneumonitis and promote pulmonary fibrosis; inflammatory monocytes, which are bone marrow derived and express CCR2, have been shown to migrate into the lung after radiation exposure. Although the extent to which recruited inflammatory monocytes contribute to radiation-induced pulmonary fibrosis has not been fully investigated, we hypothesize that its pathogenesis is reliant on this population. The CC chemokine ligand, CCL2, is a chemotactic mediator responsible for trafficking of CCR2+ inflammatory cells into the lung. Therefore, the contribution of this mediator to fibrosis development was analyzed. Interleukin (IL)-1β, a potent pro-inflammatory cytokine expressed during the radiation response, and its receptor, IL-1R1, were also evaluated. To this end, CCR2-/-, IL-1β-/- and IL-1R1-/- chimeric mice were generated and exposed to 12.5 Gy thoracic radiation, and their response was compared to wild-type (C57BL/6) syngeneic controls. Fibrotic foci were observed in the periphery of the lungs of C57 syngeneic mice and CCR2-/- recipient mice that received C57 bone marrow (C57 > CCR2-/-) by 16 and 12 weeks after irradiation, respectively. In contrast, in the mice that had received bone marrow lacking CCR2 (CCR2-/- > C57 and CCR2-/- syngeneic mice), no pulmonary fibrosis was observed at 22 weeks postirradiation. This observation correlated with decreased numbers of infiltrating and interstitial macrophages compared to controls, as well as reduced proportions of pro-inflammatory Ly6C+ macrophages observed at 12-18 weeks postirradiation, suggesting that CCR2+ macrophages contribute to radiation-induced pulmonary fibrosis. Interestingly, reduced proportions of CD206+ lung macrophages were also present at these time points in CCR2-/- chimeric mice, regardless of donor bone marrow type, suggesting that the phenotype of resident subsets may be influenced by CCR2. Furthermore, chimeras, in which either IL-1β was ablated from infiltrating cells or IL-1R1 from lung tissues, were also protected from fibrosis development, correlating with attenuated CCL2 production; these data suggest that IL-1β may influence chemotactic signaling after irradiation. Overall, our data suggest that CCR2+ infiltrating monocyte-derived macrophages may play a critical role in the development of radiation-induced pulmonary fibrosis."
      }
    },
    computed: {
      json() {
        try {
          return JSON.parse(this.input);
        } catch (e) {
          return []
        }
      },
      words() {
        return this.json.map(obj => obj.Word);
      },
      noWords() {
        return this.words.length === 0;
      },
      highlightedContent() {
        if(this.noWords) {
          return this.content;
        }

        let highlightedContent = this.content;

        this.words.forEach(word => {
          highlightedContent = highlightedContent.replace(new RegExp(word, "gi"), match => {
            return '<span class="highlightText">' + match + '</span>';
          })
        });

        return highlightedContent;
      }
    },
    methods: {
      highlight() {

      }
    }
  };
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  .highlightText {
    background: yellow;
  }
</style>