# Projeto de Semáforo Inteligente, em SPRINTS.

## <pre>Feito por: [Nicoly Ribeiro](http://github.com/nicolyribeiroo7 "Nicoly Ribeiro"), [Mariana Ribeiro](http://github.com/MarianaRibeiro07 "Mariana Ribeiro"), <br>[Eduardo Zanetti](http://github.com/Z4nettx "Eduardo Zanetti"), [Rafael Brecci](http://github.com/rbrecci "Rafael Brecci") e [Nicolas Fernandes](http://github.com/NickSantos18 "Nicolas Fernandes").

<br>

# **_Semáforo Inteligente - StartDev_**

## SPRINT 1

### Na Sprint 1, nós, da StartDev, idealizamos nosso projeto, como pode se ver na [documentação da Sprint](./SPRINT1/ProjetoSemaforoInteligenteSPRINT1.pdf).

#### Neste documento, detalhamos o nosso desejo em combater o grande trânsito na cidade, por meio de um semáforo inteligente, que inicialmente, funcionaria através de sensores. O código utilizado na programação seria C++, por meio do microcomputador Arduino.

<hr>

## SPRINT 2

### Na Sprint 2, obtivemos experiência manual com o Arduino, adquirindo melhor entendimento de como prosseguir com o projeto.

#### Com o Arduino em mãos, pôde-se adicionar requisitos funcionais e não funcionais no projeto, como queríamos na [Sprint 1](./SPRINT1/). Isto é, sensores de movimento para pedestres e carros, entre outros.

#### Além disso, foi possível fazer uma lista de materiais para a execução do projeto, como: Sensor Ultrasônico (HR-SR04); LED's; Resistores e Fios para a instalação do circuito, além de claro, o Arduino UNO.

#### Segue a representação do estágio atual do projeto, por TinkerCad.

![Image](https://github.com/user-attachments/assets/a29fe9b6-e228-4731-85fb-1845548074f2)

#### Representação do funcionamento com Sensor Ultrasônico:

![Image](https://github.com/user-attachments/assets/74603f4b-a4de-465f-bfc4-6e33259ead2d)

<hr>

## SPRINT 3

### Na Sprint 3, começamos o protótipo da maquete, feito no aplicativo Paint. Logo após, começamos o trabalho da maquete. Com ele, vieram desafios. Mudamos um pouco o trajeto que estávamos seguindo e decidimos adicionar algumas coisas.

#### O projeto no início, tinha apenas como objetivo fazer o semáforo com sensor ultrasônico e com botão. Agora, tinhamos então, como objetivo, fazer:

<ul>
<em>
<li> Um semáforo inteligente, com sensor ultrasônico; </li>
<br>
<li> Um semáforo automático, funcionando perfeitamente, e mudando através da solicitação de preferência feita pelo pedestre; </li>
<br>
<li> Uma situação de acidente: um semáforo sinalizando alerta, e uma viatura de polícia para averiguar o ocorrido. </li>
<br>
<li> <strong>Observação: a equipe optou por juntar as programações da viatura de polícia e do semáforo em situação de acidente. </strong>
</em>
</ul>
<br>

#### Com isso, começamos então a realizar o circuito via [TinkerCad.](https://www.tinkercad.com/) Embora existam sim algumas limitações, ele ajudou a equipe a ter uma noção de onde iriam ficar os fios, e pode-se então, adaptar possibilidades, como não usar por exemplo, resistores na montagem da maquete, visto que não tinha necessidade (algo que não poderia ser feito em TinkerCad).

#### Além disso, precisamos usar 3 'Arduino Uno' no circuito TinkerCad (O que não ocorreria na maquete real), por conta de diferentes programações que tivemos que implementar.

#### Portanto, o estágio atual, em TinkerCad, do projeto, ficou assim:

https://github.com/user-attachments/assets/233aabe3-3c35-4edc-ad0b-1a2d5e250ef5 <!-- video -->

#### Segue também, algumas fotos de como ocorreu a confecção da maquete:

<p align="justify">
  <img src="https://github.com/user-attachments/assets/310d8352-3d42-456f-9fc9-4789fbeb1441" alt="Confecção Maquete 1" />
  <br> <br> <br>
  <img src="https://github.com/user-attachments/assets/dce27c27-98d0-4907-bb63-fbe54e09d2cc" alt="Confecção Maquete 2" />
  <br> <br> <br>
  <img src="https://github.com/user-attachments/assets/1832442a-a3f6-4393-a0c2-3c134ea6e872" alt="Confecção Maquete 3" />
  <br> <br> <br>
  <img src="https://github.com/user-attachments/assets/98e6cce6-47ee-49f6-b135-9139f1f33198" alt="Confecção Maquete 4" />
  <br> <br> <br>
</p>
 

#### E a programação completa no TinkerCad:

<pre> 
// PROGRAMAÇÃO: SEMÁFORO DE CARROS E PEDESTRES COM SENSOR ULTRASÔNICO 

long cm = 0;
int vermelhoS = 7;
int amarelo = 4;
int verdeS = 3;
int vermelhoP = 6;
int verdeP = 5;

long readUltrasonicDistance(int triggerPin, int echoPin) {
  pinMode(triggerPin, OUTPUT);
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);

  pinMode(echoPin, INPUT);
  long duration = pulseIn(echoPin, HIGH);
  return (duration * 0.01723);
}

void setup() {
  Serial.begin(9600);
  pinMode(7, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
}

void loop() {
  cm = readUltrasonicDistance(13, 12);
  Serial.println(cm); // Mostra a distância no monitor serial (opcional para teste)

  if (cm <= 15) {
    // fechar carros abrir pedestres
    digitalWrite(vermelhoS, HIGH);
    digitalWrite(amarelo, LOW);
    digitalWrite(verdeS, LOW);
    digitalWrite(vermelhoP, LOW);
    digitalWrite(verdeP, HIGH);
  } else if (cm > 15 && cm < 20) {
    // passa pelo amarelo, fecha depois e fica verde
    digitalWrite(amarelo, HIGH);
    digitalWrite(verdeS, LOW);
    digitalWrite(vermelhoS, LOW);
    digitalWrite(vermelhoP, HIGH);
    digitalWrite(verdeP, LOW);
    delay(3000);

    digitalWrite(vermelhoS, HIGH);
    digitalWrite(amarelo, LOW);
    digitalWrite(verdeS, LOW);
    digitalWrite(vermelhoP, LOW);
    digitalWrite(verdeP, HIGH);
    delay(10000);
  } else {
    digitalWrite(vermelhoS, LOW);
    digitalWrite(amarelo, LOW);
    digitalWrite(verdeS, HIGH);
    digitalWrite(verdeP, LOW);
    digitalWrite(vermelhoP, HIGH);
  }
}
</pre>

<pre>
// SEMÁFORO DE CARROS E PEDESTRES COM BOTÃO

volatile bool pedidoPedestre = false;

void setup() {
  
// semaforo
  
pinMode(7, OUTPUT); // vermelho
pinMode(4, OUTPUT); // amarelo
pinMode(3, OUTPUT); // verde
  
// pedestre
  
pinMode(6, OUTPUT); // vermelho
pinMode(5, OUTPUT); // verde
  
//botao
  
pinMode(2, INPUT_PULLUP);
attachInterrupt(digitalPinToInterrupt(2),
botaoPressionado, FALLING);
digitalWrite(3, HIGH);
digitalWrite(6, HIGH);
digitalWrite(5, LOW);
}

void loop() {
if (!pedidoPedestre) {
} else {
digitalWrite(3, LOW);
digitalWrite(4, HIGH);
digitalWrite(7, LOW);
digitalWrite(6, HIGH);
digitalWrite(5, LOW);

delay(1000);
digitalWrite(4, LOW);
digitalWrite(7, HIGH);
digitalWrite(3, LOW);
digitalWrite(6, LOW);
digitalWrite(5, HIGH);
delay(3500);


digitalWrite(7, HIGH);
digitalWrite(4, LOW);
digitalWrite(3, LOW);
digitalWrite(6, LOW);
digitalWrite(5, HIGH);
pedidoPedestre = false;
delay(2000);
digitalWrite(4, LOW);
digitalWrite(7, LOW);
digitalWrite(3, HIGH);
digitalWrite(6, HIGH);
digitalWrite(5, LOW);
}
delay(100);
}

void botaoPressionado() {
pedidoPedestre = true;
}

</pre>

<pre>
// PROGRAMAÇÃO DO SEMÁFORO EM SITUAÇÃO DE ACIDENTE, JUNTO ÀS LUZES DA SIRENE DA VIATURA DE POLÍCIA:

void setup() {
  
// semaforo
  
pinMode(7, OUTPUT); // vermelho
pinMode(4, OUTPUT); // amarelo
pinMode(3, OUTPUT); // verde
  pinMode(11, OUTPUT); // vermelho
pinMode(10, OUTPUT); // azul
  
// pedestre
  
pinMode(6, OUTPUT); // vermelho
pinMode(5, OUTPUT); // verde
  
// carro de policia
  pinMode(11, OUTPUT); // vermelho
  pinMode(10, OUTPUT); // azul
  
  
}
void loop() {
  // semaforo acidente
  digitalWrite(6, HIGH);
 
  digitalWrite(7, HIGH);
  delay(250);
  digitalWrite(7, LOW);
  delay(250);
  digitalWrite(7, HIGH);
  delay(250);
  
  // carro de policia
  
  delay(100);
  digitalWrite(11, HIGH);
  digitalWrite(10, LOW);
  delay(600);
  digitalWrite(11, LOW);
  digitalWrite(10, HIGH);
}
</pre>
<br>

### Executando as programações e os testes do Arduino na maquete, conseguimos então:
<ul>
<em>
<li> Usar apenas um Arduino na parte de baixo da maquete, junto com também apenas uma protoboard; </li>
<li> Conectar os fios e colocar eles no </li>
