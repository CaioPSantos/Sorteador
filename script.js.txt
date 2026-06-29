let totalSorteios = 0;

const historico = [];

function sortear(){

const minimo = Number(document.getElementById("minimo").value);

const maximo = Number(document.getElementById("maximo").value);

if(isNaN(minimo) || isNaN(maximo)){

alert("Preencha os dois campos.");

return;

}

if(minimo>=maximo){

alert("O número mínimo deve ser menor que o máximo.");

return;

}

const resultado = document.getElementById("resultado");

resultado.innerHTML="🎲";

let contador=0;

const animacao=setInterval(()=>{

resultado.innerHTML=Math.floor(Math.random()*(maximo-minimo+1))+minimo;

contador++;

if(contador>=20){

clearInterval(animacao);

const numero=

Math.floor(

Math.random()*(maximo-minimo+1)

)+minimo;

resultado.innerHTML=numero;

resultado.style.transform="scale(1.3)";

setTimeout(()=>{

resultado.style.transform="scale(1)";

},250);

totalSorteios++;

document.getElementById("contador").innerHTML=totalSorteios;

historico.unshift(numero);

if(historico.length>10){

historico.pop();

}

atualizarHistorico();

}

},60);

}

function atualizarHistorico(){

const lista=document.getElementById("listaHistorico");

lista.innerHTML="";

historico.forEach((numero,index)=>{

lista.innerHTML+=`

<li>

#${historico.length-index}

→ ${numero}

</li>

`;

});

}

function copiarNumero(){

const numero=document.getElementById("resultado").innerText;

navigator.clipboard.writeText(numero);

alert("Número copiado!");

}

document.addEventListener("keypress",function(e){

if(e.key==="Enter"){

sortear();

}

});