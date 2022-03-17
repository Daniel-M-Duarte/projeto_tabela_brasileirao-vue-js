<template>
    <v-container>
         <h2 class="text-h5 text-center mb-3 mt-5">
            Classificação
        </h2>

        <v-simple-table>
            <template v-slot:default>
            <thead>
                <tr>
                    <th colspan="2" class="text-left">
                        Clubes
                    </th>
                    <th class="text-right">
                        Pontos
                    </th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(clubes, index) of clubesListaOrdenada" :key="clubes.id">
                    <td>{{ index +1 }}</td>
                    <td>  
                        <v-avatar size="24" >
                            <img
                                    :src="clubes.escudo"
                                    :alt="clubes.nome"
                            >
                        </v-avatar>
                        <span cclass="pr-2">{{ clubes.nome}}</span>
                    </td>
                    <td class="text-right">{{clubes.pontos}}</td>
                </tr>
            </tbody>
            </template>
        </v-simple-table>

    </v-container>    
</template>

<script>
export default {
    name: 'ClubesLista',
    data(){
        return {
            clubesLista:[]
        }
    },
    computed: {
        clubesListaOrdenada() {
            const listaOrdenada = this.clubesLista.slice(0).sort(
                (a,b) => a.pontos > b.pontos ? -1 : 1
            );
            return listaOrdenada;
        }
    },
    created() {
        fetch('https://hackthon-decola.firebaseio.com/clubes-lista.json')
            .then(resposta => resposta.json())
            .then(json => {
                this.clubesLista = json;
                console.log(this.clubesLista)
            });                
        }
    }    

</script>

<style scoped>

</style>