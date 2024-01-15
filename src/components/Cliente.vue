<!--                        Aula 256 Como criar e usar componentes 
                            Aula 257 Reatividade 
                            Aula 258 Data Binding 
                            Aula 259 Two way data binding com v-model 
                            Aula 260 Props 06/09/23
                            Aula 261 Diretivas condicionais V-if  
                            Aula 262 Classes Condicionais 
                            Aula 264 Eventos 10/09/23
                            Aula 267 Emissão de Eventos 
                            Aula 268 Filtros 23/09/23 
                            Aula 269 Computer Properties 
                            -->
<!--(1-260)-->
<template>
    <!-- Para criar várias tags, preciso encapsular no elemento pai-->
    
    <!--(2-260) Props -->
    <!--(12-262) Caso o cliente seja premium, na div dele terá essa classe (cliente-premium)
    Caso não seja tenha a classe normal (cliente)-->
    <!--adicionar a classe [cliente, quando isPremium for falso], quando is [Premium for verdadeiro use cliente-premium] * -->
        <div :class="{'cliente': !isPremium, 'cliente-premium': isPremium}">
            <h1 class="h1">PROPS</h1>
            <hr>
            <h4>NOME: {{cliente.nome }}</h4>
    <!--(18-268) Inserir o símbolo de pipe e chamar o valor de filtro(value) 17-268-->
            <p>EMAIL: {{cliente.email | processarEmail}}</p>
        <!--(8-261) Quando for true, exibe a idade-->
            <p v-if="showIdade === true">IDADE: {{cliente.idade}}</p>
        <!--(9-261) Quando for false, exibe uma mensagem-->
            <p v-else> O usuário escondeu a idade!</p>


            
    <!--(14-264) Vou disparar um evento quando o botão for clicado e vai mudar o valor da variável
    'cliente': !isPremium, 'cliente-premium': isPremium-->
            <button @click="mudarCor($event)">Mudar cor!</button>

    <!--(15-267) Criando Botão Deletar que vai ter um evento de click Estou chamando o método emitirEventoDelete(16-267)-->
            <button @click="emitirEventosDelete">Deletar</button>
    <!--(20-269)-->
            <h4>Id especial: {{ idEspecial }}</h4>
        </div>        
    </template>
    <!--(3-260) (SCRIPT) Vou definir variáveis, métodos e funções para serem chamadas dentro do meu componente-->
    <script>
    export default {
    /*(4-260) Definindo Funções Data que retorna um objeto*/
        data(){
            return{
            /*(11-262) Definindo variável, pode ser tanto true como false*/
                isPremium: true
            }
        },
    /*(5-260) [Prop do tipo (STRING)] 
    Vou criar um objeto chamadoo props, e dentro dele eu vou definir os atributos que vou receber */
        props: {
            cliente: Object,
    /*(7-261) Objeto showIdade */
            showIdade: Boolean
        },
    // /*(13-264) Criando um método/Objeto methods e passando uma função */
        methods : {
            mudarCor: function($event){
                console.log("Chamando Evento")
                console.log($event)
                // ispremium recebe ela mesma invertida
                this.isPremium = !this.isPremium;
            },
    /*(16-267) Criar um método para para deletar  */
        emitirEventosDelete: function(){
            console.log("Emitindo do Filho");
    // Posso passar um segundo parametro que é um objeto
            this.$emit("meDelete",{idDoCliente: this.cliente.id,curso: "Formação Node.js", emPromocao: true, component: this});
        }           
    },
    /*(17-268) Vou criar um filtro que recebe por padrão um valor = value  */
    filters:{
        processarEmail: function(value){
            // Um filtro sempre me retorna algo
            return value.toUpperCase();
        }
    },
    /*(19-269) Criar um novo objeto*/
    computed: {
        // Definindo um método chamado de idEspecial
        idEspecial: function(){
            // Me retonra um valor (String) que é a união de email + nome + id, vou deixar em letra maiúscula
            return (this.cliente.email + this.cliente.nome + this.cliente.id).toUpperCase();
        }
    }
}
    
    </script>
    <!--() (CSS) Aqui vou definir o css do meu componente, o atributo (SCOPED) diz que tudo oque for aplicado nessa
    tag de estilo, só vai ser aplicado nesse componente  -->

    <style scoped>
      
        .cliente{
            background-color: rgba(138, 2, 138, 0.377);
            padding: 2%;
            max-width: 500px;

            margin-top: 2%;
        }
        h1{
            text-align: center;
            padding: 10px;
            font-size: 2.5rem;
        }
        p{
            font-style: inherit;
        }

        /*(10-262) */
        .cliente-premium{
            background-color: black;
            color: yellow;
            padding: 2%;
            max-width: 500px;
            margin-top: 2%;
        }
        
        
     
    </style>