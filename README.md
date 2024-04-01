# CP1-edge
#c++

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
