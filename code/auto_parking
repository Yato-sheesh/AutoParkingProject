#include <Stepper.h>
#include <Arduino.h>
#include <NewPing.h>

#define PIN_TRIG A0
#define PIN_ECHO A1

#define MAX_DISTANCE 200 // Константа для определения максимального расстояния, которое мы будем считать корректным.

// Создаем объект, методами которого будем затем пользоваться для получения расстояния.
// В качестве параметров передаем номера пинов, к которым подключены выходы ECHO и TRIG датчика

NewPing sonar(PIN_TRIG, PIN_ECHO, MAX_DISTANCE);

int y = 0;
int i = 0;
int numplace = 0;
int num_func = 0;
int freeplace[6] = {0, 0, 0, 0, 0, 0}; // массив для проверки наличия куар кода
char numA[6] = {0, 0, 0, 0, 0, 0}; // массив для номеров автомобиля
unsigned int distance = sonar.ping_cm();
const int stepsPerRevolution = 2048;
const int step_for_free = 2048;

Stepper stepper3(stepsPerRevolution, 4, 5, 6, 7);
Stepper stepper2(stepsPerRevolution, 8, 9, 10, 11);
Stepper stepper1(stepsPerRevolution, A2, A3, A4, A5);

void setup() {
  Serial.begin(115200);
  Serial.println();
  stepper1.setSpeed(13);
  stepper2.setSpeed(13);
  stepper3.setSpeed(13);
}

void InputConv(){
  while (distance > 3){
    delay(50);
    // Получаем значение от датчика расстояния и сохраняем его в переменную
    distance = sonar.ping_cm();
    // Печатаем расстояние в мониторе порта
    Serial.print(distance);
    Serial.println("см");
    stepper1.step(256); 
  }
}
void PlacesStepTo1(){
 stepper2.step(-step_for_free * i);
 y = 0;
}

void PlacesStepTo2(){
 stepper2.step(-step_for_free * (i-1));
 y = 1;
}

void PlacesStepTo3(){
 stepper2.step(-step_for_free * (i-2));
 y = 2;
}

void PlacesStepTo4(){
 stepper2.step(-step_for_free * (i-3));
 y = 3;
}

void PlacesStepTo5(){
 stepper2.step(-step_for_free * (i-4));
 y = 4;
}

void PlacesStepTo6(){
 stepper2.step(-step_for_free * (i-5));
 y = 5;
}

void TofreePlace(){
  stepper2.step(2048);
  if (y < 6){
    y += 1;
  }
  else if (y == 6){
    y = 0;
  }
}

void Output(){
  for (int y = 0; y<10000; y++){
    stepper3.step(128);
    }
}


void loop(){
  if  (Serial.available() > 0){ 
    String  i  =  Serial . readStringUntil ( '\n' ) ; 
    Serial . println ( "Получено: "  +  i ) ; 
  } 
  if (i != 0){                                       //проверка на наличие таких же QR
    if ((freeplace[0] == 1) && (numA[0] == i)){
      numA[0] = 0;
      freeplace[0] = 0;
      Serial.print("QR-код на автомобиле: ");
      Serial.println(i);
      Serial.print("Машина выехала из ячейки: ");
     Serial.println("1");
    i = 0;
    num_func = 7;
    }

    else if ((freeplace[1] == 1) && (numA[1] == i)){
      numA[1] = 0;
      freeplace[1] = 0;
      Serial.print("QR-код на автомобиле: ");
      Serial.println(i);
      Serial.print("Машина выехала из ячейки: ");
      Serial.println("2");
      i = 0;
      num_func = 8;
    }   

    else if ((freeplace[2] == 1) && (numA[2] == i)){
     numA[2] = 0;
      freeplace[2] = 0;
      Serial.print("QR-код на автомобиле: ");
     Serial.println(i);
      Serial.print("Машина выехала из ячейки: ");
      Serial.println("3");
      i = 0;
      num_func = 9;
    }

    else if ((freeplace[3] == 1) && (numA[3] == i)){
      numA[3] = 0;
      freeplace[3] = 0;
      Serial.print("QR-код на автомобиле: ");
      Serial.println(i);
      Serial.print("Машина выехала из ячейки: ");
      Serial.println("4");
     i = 0;
     num_func = 10;
    }

    else if ((freeplace[4] == 1) && (numA[4] == i)){
     numA[4] = 0;
      freeplace[4] = 0;
      Serial.print("QR-код на автомобиле: ");
     Serial.println(i);
     Serial.print("Машина выехала из ячейки: ");
      Serial.println("5");
     i = 0;
     num_func = 11;
    }
    
    else if ((freeplace[5] == 1) && (numA[5] == i)){
      numA[5] = 0;
      freeplace[5] = 0;
     Serial.print("QR-код на автомобиле: ");
     Serial.println(i);
      Serial.print("Машина выехала из ячейки: ");
      Serial.println("6");
      i = 0;
      num_func = 12;
    }
  

    else if (freeplace[0] == 0){                         //присваение QR ячейке
      numA[0] = i;
      freeplace[0] = 1;
      Serial.print("QR-код на автомобиле: ");
     Serial.println(i);
      Serial.print("Номер ячейки хранения автомобиля ");
      Serial.println("1");
      i = 0;
      num_func = 1;
    }

   else if (freeplace[1] == 0){
     numA[1] = i;
     freeplace[1] = 1;
      Serial.print("QR-код на автомобиле: ");
      Serial.println(i);
     Serial.print("Номер ячейки хранения автомобиля ");
      Serial.println("2");
     i = 0;
     num_func = 2;
    }

    else if (freeplace[2] == 0){
     numA[2] = i;
      freeplace[2] = 1;
      Serial.print("QR-код на автомобиле: ");
     Serial.println(i);
      Serial.print("Номер ячейки хранения автомобиля ");
     Serial.println("3");
     i = 0;
     num_func = 3;
    }

    else if (freeplace[3] == 0){
     numA[3] = i;
     freeplace[3] = 1;
      Serial.print("QR-код на автомобиле: ");
      Serial.println(i);
     Serial.print("Номер ячейки хранения автомобиля: ");
      Serial.println("4");
     i = 0;
     num_func = 4;
   }

    else if (freeplace[4] == 0){
    numA[4] = i;
    freeplace[4] = 1;
    Serial.print("QR-код на автомобиле: ");
    Serial.println(i);
    Serial.print("Номер ячейки хранения автомобиля ");
    Serial.println("5");
    i = 0;
    num_func = 5;
    }

   else if (freeplace[5] == 0){
      numA[5] = i;
      freeplace[5] = 1;
      Serial.print("QR-код на автомобиле: ");
     Serial.println(i);
     Serial.print("Номер ячейки хранения автомобиля ");
      Serial.println("6");
      i = 0;
      num_func = 6;
    }
    else{
      Serial.println("Ошибка");
    }
  }

// функция загрузки и выгрузки
  if (num_func == 1){
    Serial.println("Разрешена загрузка");
    delay(1000);
    InputConv();
    Serial.println("Загрузка прошла успешно");
    delay(1000);
    Serial.println("Хранение");
    TofreePlace();
    Serial.println("Операция выполнена");
    num_func = 0;
    }
  else if (num_func == 2){
    Serial.println("Разрешена загрузка");
    delay(1000);
    InputConv();
    Serial.println("Загрузка прошла успешно");
    delay(1000);
    Serial.println("Хранение");
    TofreePlace();
    Serial.println("Операция выполнена");
    num_func = 0;
    }
  else if (num_func == 3){
    Serial.println("Разрешена загрузка");
    delay(1000);
    InputConv();
    Serial.println("Загрузка прошла успешно");
    delay(1000);
    Serial.println("Хранение");
    TofreePlace();
    Serial.println("Операция выполнена");
    num_func = 0;
    }
  else if (num_func == 4){
    Serial.println("Разрешена загрузка");
    delay(1000);
    InputConv();
    Serial.println("Загрузка прошла успешно");
    delay(1000);
    Serial.println("Хранение");
    TofreePlace();
    Serial.println("Операция выполнена");
    num_func = 0;
    }
  else if (num_func == 5){
    Serial.println("Разрешена загрузка");
    delay(1000);
    InputConv();
    Serial.println("Загрузка прошла успешно");
    delay(1000);
    Serial.println("Хранение");
    TofreePlace();
    Serial.println("Операция выполнена");
    num_func = 0;
    }
  else if (num_func == 6){
    Serial.println("Разрешена загрузка");
    delay(1000);
    InputConv();
    Serial.println("Загрузка прошла успешно");
    delay(1000);
    Serial.println("Хранение");
    TofreePlace();
    Serial.println("Операция выполнена");
    num_func = 0;
    }


  else if (num_func == 7){
    Serial.println("Установка готова к вращению ячеек");
    delay(1000);
    PlacesStepTo1();
    delay(1000);
    Serial.println("Разрешена выгрузка");
    delay(1000);
    Output();
    Serial.println("Выгрузка прошла успешно");
    num_func = 0;
    }
  else if (num_func == 8){
    Serial.println("Установка готова к вращению ячеек");
    delay(1000);
    PlacesStepTo2();
    delay(1000);
    Serial.println("Разрешена выгрузка");
    delay(1000);
    Output();
    Serial.println("Выгрузка прошла успешно");
    num_func = 0;
    }
  else if (num_func == 9){
    Serial.println("Установка готова к вращению ячеек");
    delay(1000);
    PlacesStepTo3();
    delay(1000);
    Serial.println("Разрешена выгрузка");
    delay(1000);
    Output();
    Serial.println("Выгрузка прошла успешно");
    num_func = 0;
    }
  else if (num_func == 10){
    Serial.println("Установка готова к вращению ячеек");
    delay(1000);
    PlacesStepTo4();
    delay(1000);
    Serial.println("Разрешена выгрузка");
    delay(1000);
    Output();
    Serial.println("Выгрузка прошла успешно");
    num_func = 0;
    }
  else if (num_func == 11){
    Serial.println("Установка готова к вращению ячеек");
    delay(1000);
    PlacesStepTo5();
    delay(1000);
    Serial.println("Разрешена выгрузка");
    delay(1000);
    Output();
    Serial.println("Выгрузка прошла успешно");
    num_func = 0;
    }
  else if (num_func == 12){
    Serial.println("Установка готова к вращению ячеек");
    delay(1000);
    PlacesStepTo6();
    delay(1000);
    Serial.println("Разрешена выгрузка");
    delay(1000);
    Output();
    Serial.println("Выгрузка прошла успешно");
    num_func = 0;
    }

  delay(2000);
}
