# CP1-edge
#c++

int RED = 2; // Define o pino para o LED vermelho
int YELLOW = 3; // Define o pino para o LED amarelo
int GREEN = 4; // Define o pino para o LED verde
int BUZZER = 5; // Define o pino para o buzzer
int Sensor = A0; // Define o pino para o sensor de luz

void setup() {
  Serial.begin(9600); // Inicializa a comunicação serial com uma taxa de 9600 baud
  pinMode(RED, OUTPUT); // Define o pino do LED vermelho como saída
  pinMode(YELLOW, OUTPUT); // Define o pino do LED amarelo como saída
  pinMode(GREEN, OUTPUT); // Define o pino do LED verde como saída
  pinMode(BUZZER, OUTPUT); // Define o pino do buzzer como saída
  pinMode(Sensor, INPUT); // Define o pino do sensor de luz como entrada
}

void loop() {
  int sensorValue = analogRead(Sensor); // Lê o valor analógico do sensor de luz
  int i = map(sensorValue, 54, 974, 0, 100); // Mapeia o valor do sensor para uma escala de 0 a 100
  Serial.println(sensorValue); // Imprime o valor do sensor no monitor serial
  Serial.println(i); // Imprime o valor mapeado no monitor serial
  delay(1000); // Aguarda 1 segundo
  
  // Controle dos LEDs e do buzzer baseado no valor mapeado
  if(i < 20){ // Se o valor mapeado for menor que 20
    // Iluminação OK, acende o LED verde
    digitalWrite(GREEN, HIGH);
  } else {
    // Caso contrário, apaga o LED verde
    digitalWrite(GREEN, LOW);
  }

  if(i >= 21 && i <= 70){ // Se o valor mapeado estiver entre 21 e 70
    // Iluminação em níveis de alerta, acende o LED amarelo
    digitalWrite(YELLOW, HIGH);
  } else {
    // Caso contrário, apaga o LED amarelo
    digitalWrite(YELLOW, LOW);
  }
 
  if(i > 71){ // Se o valor mapeado for maior que 71
    // Indicando que há um problema, acende o LED vermelho e o buzzer
    digitalWrite(RED, HIGH);
    digitalWrite(BUZZER, HIGH);
  } else {
    // Caso contrário, apaga o LED vermelho e o buzzer
    digitalWrite(RED, LOW);
    digitalWrite(BUZZER, LOW);
  }
}
