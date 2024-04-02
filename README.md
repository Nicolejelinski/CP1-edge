# Sistema de Monitoramento de Ambiente para Vinheria Agnello:
Este é um projeto desenvolvido para a Vinheria Agnello, com o objetivo de monitorar as condições no armazenamento de vinhos. O sistema utiliza sensores para medir a luminosidade, e sinaliza qualquer desvio do limite estipulado por meio de LEDs e um buzzer.

# Funcionalidades:
O sistema monitora a seguinte grandeza:
Luminosidade.
Utiliza um LED verde para indicar que a grandeza está dentro dos limites estipulados.
Utiliza um LED amarelo para indicar que há um nível de alerta na grandeza.
Utiliza um LED vermelho para indicar que há um problema grave na grandeza.
Quando a grandeza está em nível de alerta, um buzzer soa por 3 segundos. O buzzer volta a soar caso a luminosidade permaneça em nível de alerta.


# Componentes Necessários:
Arduino Uno R3;
Protoboard;
Led Verde;
Led Vermelho;
Led Amarelo;
Buzzer;
Sensor de luminosidade(LDR);
3 Resistores(220Ω);
Resistor(10kΩ).

# Instalação
# Hardware:
Conecte o sensor de luminosidade(LDR) ao Arduino.
Conecte o LDR com o resistor de 10kΩ.
Conecte os LEDs amarelo, verde e vermelho, e o buzzer, ao Arduino conforme definido no código.
Conecte os LEDs com os resistores de 220Ω.
Certifique-se de conectar o buzzer a um pino PWM adequado no seu Arduino.

# Software:
Abra o arquivo do código-fonte em um ambiente de desenvolvimento integrado para Arduino (como Arduino IDE).
Carregue o código no Arduino.

# Limites Estipulados:

Os limites de luminosidade podem variar de acordo com as especificidades do ambiente de armazenamento de vinhos. No código fornecido, os limites são definidos, mas podem ser ajustados conforme necessário.

# Alimentação:

Certifique-se de alimentar o Arduino com uma fonte de energia apropriada, como uma porta USB do computador ou uma fonte de alimentação externa.

# Teste:

Após carregar o código no Arduino e conectar todos os componentes, teste o sistema de monitoramento para garantir que os LEDs e o buzzer estejam funcionando corretamente.
Observe as alterações no comportamento dos LEDs e do buzzer conforme a luminosidade ambiente varia.


# Autores 
Este projeto foi desenvolvido pela equipe de desenvolvedores contratada pela Vinheria Agnello:
Nicolle Pellegrino Jelinski Rodrigues RM558610;
Felipe Genistretti Rodrigues RM556348;
Renan Simões Gonçalves RM555584;
Gabriel Guilherme  RM558638.




# CP1-edge
# c++
```c++
// Definição dos pinos para os componentes conectados ao Arduino
int RED = 2;        // Pino do LED vermelho
int YELLOW = 3;     // Pino do LED amarelo
int GREEN = 4;      // Pino do LED verde
int BUZZER = 5;     // Pino do buzzer
int Sensor = A0;    // Pino do sensor de luz

void setup() {
  // Inicialização da comunicação serial para depuração a uma velocidade de 9600 bauds
  Serial.begin(9600);
  
  // Configuração dos pinos como entrada ou saída
  pinMode(RED, OUTPUT);      // Define o pino do LED vermelho como saída
  pinMode(YELLOW, OUTPUT);   // Define o pino do LED amarelo como saída
  pinMode(GREEN, OUTPUT);    // Define o pino do LED verde como saída
  pinMode(BUZZER, OUTPUT);   // Define o pino do buzzer como saída
  pinMode(Sensor, INPUT);    // Define o pino do sensor de luz como entrada
}

void loop() {
  // Leitura do valor analógico fornecido pelo sensor de luz
  int sensorValue = analogRead(Sensor);
  
  // Mapeia o valor lido do sensor para um intervalo de 0 a 100
  int i = map(sensorValue, 54, 974, 0, 100);
  
  // Exibe os valores lidos do sensor de luz e sua correspondência mapeada no monitor serial
  Serial.println(sensorValue); // Imprime o valor analógico lido pelo sensor
  Serial.println(i);           // Imprime o valor mapeado do sensor
  delay(1000);                 // Aguarda 1 segundo antes da próxima leitura
  
  // Controla o LED verde com base na intensidade de luz medida
  if(i < 20) { // Se a intensidade de luz for menor que 20, acende o LED verde
    digitalWrite(GREEN, HIGH);
  } else {    // Senão, apaga o LED verde
    digitalWrite(GREEN, LOW);
  }

  // Controla o LED amarelo com base na intensidade de luz medida
  if(i >= 21 && i <= 70) { // Se a intensidade de luz estiver entre 21 e 70, acende o LED amarelo
    digitalWrite(YELLOW, HIGH);
  } else {                // Senão, apaga o LED amarelo
    digitalWrite(YELLOW, LOW);
  }
 
  // Se a intensidade de luz for maior que 71, considera-se que há um problema
  if(i > 71) {
    // Ativa o LED vermelho e o buzzer
    digitalWrite(RED, HIGH);
    digitalWrite(BUZZER, HIGH);
    delay(3000);            // Mantém o buzzer ligado por 3 segundos
    digitalWrite(BUZZER, LOW); // Desliga o buzzer
    delay(2000);            // Espera 2 segundos
    digitalWrite(BUZZER, HIGH); // Liga novamente o buzzer
  } else {
    // Se a intensidade de luz for menor ou igual a 71, apaga o LED vermelho e o buzzer
    digitalWrite(RED, LOW);
    digitalWrite(BUZZER, LOW);
  }
}
```
