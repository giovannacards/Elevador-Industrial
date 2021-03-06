# Elevador Industrial


Ao pensar em um elevador automaticamente é imaginado um mecanismo feito para apenas subir e descer em vertical, o comum que encontramos em prédios e comércios. Entretanto a existência de elevadores que também se movimentam no eixo X inspirou o grupo a criar um protótipo que realiza ambos os movimentos, nosso **"Elevador Industrial".**


Ao pensar no projeto, o objetivo inicial é fazer um grande mecanismo que conseguisse mover um caixote na vertical e horizontal para a posição desejada. O elevador teria fusos conectados em motores, que ao girar iriam fazer a intersecção entre os eixos X e Y se movimentar. Nesta, existiria um caixote de madeira que seria a parte de levar os objetos do elevador, e poderia então se mover em qualquer coordenada dentro da caixa. 


---

## Lista de materiais
- 2 motores de passo Nema 17;
- 2 fuso trapezoidal de 500mm e passo de 8mm;
- 2 castanhas para ser usada no fuso;
- 2 acoplamentos flexíveis;
- 2 mancais;
- 1 estrutura fixa de madeira 300x300mmm;
- 1 caixote de madeira;
- 4 hastes de ferro;
- 2 suportes para cada uma das castanhas;
- 1 arduino Uno com USB;
- 1 driver A4988;
- Jumpers;
- 1 capacitor de 25v 230mf;
- 1 fonte de energia de 12v 10A;
- Parafusos; 
- Fita Isolante.




---

## Montagem

Transferidor de Eixo = Intersecção de Eixo

1. O primeiro passo foi fazer a estrutura de madeira com medida aproximada de 300mm x 300mm, esta tinha que ser estável e não ter fundo, por conta dos eixos, sendo apenas a estrutura.

2. O segundo passo foi medir o projeto e delimitar o local de cada fuso, motor e em como iria andar ambas as hastes da intersecção. As definições foram feitas usando régua, trena e paquímetro.

3. Quando a estrutura estava pronta e as medidas tiradas, se iniciou a construção do projeto, com a perfuração da caixa para fixar os dois fusos, em cima e outro ao lado, e em conectar as hastes nas castanhas, nesta etapa começamos a nos preocupar em como seria o “transferidor de eixo” que faria com que o caixote se movimentasse em ambas as hastes.

4. Quando tudo estava bem fixado sem comprometer a movimentação dos eixos, o trabalho com os motores começou, por serem motores de passo precisamos identificar as bobinas e como iríamos ligar ele no drive. O conectamos no Arduino e no driver A4988, usamos uma fonte de 12V / 10A para alimentá-lo.

5. Com a maior parte da estrutura pronta, os testes com ambos os motores, em sentido horário e anti-horário, usando o monitor serial do Arduino IDE, controlamos o motor. 

6. Os finais dos testes começaram, e infelizmente não saíram como deveria funcionar, já que o transferidor de eixo não funcionando como deveria, além disso um dos drivers usados para conversar com os motores queimou no meio do trabalho.


![Montagem](./img/montagem1.jpeg)

![Montagem](./img/montagem2.jpeg)

![Montagem](./img/montagem3.jpeg)




---
## Código Fonte


````
#include <AccelStepper.h>

int velocidade_motor = 3000; 
int aceleracao_motor = 3000;
int p1 = 0;
int numero = 0; 


// Definicao pino ENABLE
int pino_enable1 = 8;


// Definicao pinos STEP e DIR
AccelStepper motor1(4,3);

void setup()
{
  Serial.begin(9600);
  pinMode(pino_enable1, OUTPUT);
  // Configuracoes iniciais motor de passo
  motor1.setMaxSpeed(velocidade_motor);
  motor1.setSpeed(velocidade_motor);
  motor1.setAcceleration(aceleracao_motor);
  
  Serial.println("Digite um número de 0 a 3 e clique em ENVIAR...");
}
void loop()
{

  // Aguarda os caracteres no serial monitor
  if (Serial.available() > 0) 
  {
    numero = Serial.read();
    {
      if (numero == '1')
      {
        Serial.println("Numero 1 recebido - Posição 0...");
        digitalWrite(pino_enable1, LOW);
        p1 = 1;
      } 
      
      if (numero == '2')
      {
        Serial.println("Numero 2 recebido - Meia Barra...");
        digitalWrite(pino_enable1, LOW);
        p1 = 2;
      }
     
      if (numero == '3')
      {
        Serial.println("Numero 3 recebido - Final de Curso...");
        digitalWrite(pino_enable1, LOW)
        p1 = 3;
      } 
      
      if (numero == '0')
      {
        Serial.println("Numero 0 recebido - Parando motor...");
        p1 = 0;
        digitalWrite(pino_enable1, HIGH);
      } 
    }
  }
  
  if (p1 == 1)
  {
    motor1.moveTo(0);
  }
  
  if (p1 == 2)
  {
    motor1.moveTo(15000);
  }
  
   if (p1 == 3)
  {
    motor1.moveTo(30000);
  }
  
  motor1.run();
}
````




---

## Resultados

Os resultados do projeto não atingiram o seu propósito por completo, por conta de erros mecânicos, o “transferidor de eixo” não suportou a pressão dos fusos em seu estado de funcionamento, assim foi reportado a necessidade de um desenvolvimento e reconstrução do “transferidor de eixo”, para que assim seja possível a movimentação sem o problemas de arrasto.

--- 

### Autores do projeto
+ Allan Oliveira Cardoso de Sá
+ Fernanda de Azevedo Bastos Fernandes
+ Giovanna Gomes Cardoso 
+ Maria Eduarda da Paixão Borzani

 1⁰ Sistemas Embarcados - FATEC Jundiaí - 2022







































































