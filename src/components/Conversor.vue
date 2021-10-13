<template>
    <h1>CONVERSOR DE TEXTO PARA SHA256</h1>
    <div>
        <textarea id="txtTexto" :cols="colunas" :rows="linhas" v-model="txtTexto" placeholder="Texto a ser convertido:" >  </textarea>
    </div>
    <p></p>
    <div>
        <!-- <button @click="Converte">Converter</button> -->
        <h3>Algorítimo HASH</h3> 
        <!-- <select name="tipoHash" id="tipoHash" @change="Converte">
            <option value="0">SHA256</option>
            <option value="1">SHA512</option>
        </select> -->
        
        <div>
          <input type="radio" id="0" name="rbHASH" @click="Converte" checked> <label for="0">SHA256</label>
          <input type="radio" id="1" name="rbHASH" @click="Converte"> <label for="1">SHA512</label>
        </div>
      
        
        
    </div>
    <p></p>
    <div>
        <textarea id="txtConvertido" :cols="colunas" :rows="linhas" disabled v-model="txtConvertido">  </textarea>
    </div>
    <p></p>
    <button @click="copiaTexto">Cópiar resultado para área de transferência</button>
    

</template>

<script>

var hash = require('hash.js')
var sha512 = require('hash.js/lib/hash/sha/512')

export default {
    name: 'Conversor',
    data() {
        return {
            txtTexto: '',
            txtConvertido: '',
            colunas: 80,
            linhas: 10

        }
    },
    methods: {
        Converte() {

            if (document.getElementById('0').checked) {
                this.txtConvertido = hash.sha256().update(this.txtTexto).digest('hex')
            }
            if (document.getElementById('1').checked) {
                this.txtConvertido = sha512().update(this.txtTexto).digest('hex')
            }

            document.getElementById('txtTexto').focus
           
        },
        copiaTexto() {
            const textarea = document.createElement('textarea');
            document.body.appendChild(textarea);
            textarea.value = this.txtConvertido;
            textarea.select();
            textarea.setSelectionRange(0, 99999);
            document.execCommand('copy');
            document.body.removeChild(textarea);
            alert('Texto enviado para área de trabalho')
        }
    }, 
    watch: {
        txtTexto: function() {
            this.Converte()
        }
    }
}

</script>