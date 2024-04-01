# CP1-edge

// C++ code
// Definição dos pinos dos componentes
int RED = 2;       // Pino do LED vermelho
int YELLOW = 3;    // Pino do LED amarelo
int GREEN = 4;     // Pino do LED verde
int BUZZER = 5;    // Pino do buzzer
int Sensor = A0;   // Pino do sensor de luz (análogo A0)
void setup() {
  // Inicialização do monitor serial com a taxa de transmissão de 9600 bps
  Serial.begin(9600);
  // Configuração dos pinos dos componentes como saídas
  pinMode(RED, OUTPUT);
  pinMode(YELLOW, OUTPUT);
  pinMode(GREEN, OUTPUT); 
  pinMode(BUZZER, OUTPUT);
}
void loop() {
  // Leitura do valor analógico do sensor de luz
  int sensorValue = analogRead(Sensor);
  // Mapeamento do valor lido para um intervalo de 0 a 100
  int i = map(Sensor, 0, 1023, 0, 100);
  // Impressão do valor mapeado no monitor serial
  Serial.println(i);
  // Controle dos componentes com base no valor do sensor
  if(i < 60){
    // Se a intensidade de luz for menor que 60, acende-se o LED verde e apagam-se os LEDs amarelo e vermelho
    digitalWrite(GREEN, HIGH);
    digitalWrite(YELLOW, LOW);
    digitalWrite(RED, LOW);
  }
  else if (i > 70){
    // Se a intensidade de luz for maior que 70, acende-se o LED amarelo e apagam-se os LEDs verde e vermelho
    digitalWrite(GREEN, LOW);
    digitalWrite(YELLOW, HIGH);
    digitalWrite(RED, LOW);
  }
  else {
    // Caso contrário, acende-se o LED vermelho, apaga-se o LED amarelo, emite-se um som pelo buzzer e aguarda-se 1 segundo
    digitalWrite(GREEN, LOW);
    digitalWrite(RED, HIGH);
    digitalWrite(YELLOW, LOW);
    tone(BUZZER, 2000, 2000);
    delay(1000);
  }
  // Aguarda-se 400 milissegundos antes de repetir o processo
  delay(400);
}
