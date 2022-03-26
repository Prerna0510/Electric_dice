# Electric_dice
int piezo=13;

int pin[7]={2, 3, 4, 5, 6, 11, 12};
int dot_pattern[6][7]={
  {0, 0, 0, 1, 0, 0, 0},
  {1, 0, 0, 0, 0, 0, 1},
  {1, 0, 0, 1, 0, 0, 1},
  {1, 1, 0, 0, 0, 1, 1},
  {1, 1, 0, 1, 0, 1, 1},
  {1, 1, 1, 0, 1, 1, 1}
}; 
int face;
int lastface=10;
  
void setup()
{
  pinMode(7, INPUT_PULLUP);
  pinMode(piezo, OUTPUT);
  
  for(int i=0;i<7; i++)
  {
    pinMode(pin[i],OUTPUT);
  }
  randomSeed(analogRead(A5));
}
void throw_1()
{
  int delay_ms=1;
  while(delay_ms<200)
  {
    do{
      face=random(6);
    }while(face==lastface);
    lastface=face;
    for(int dot=0; dot<7; dot++)
    {
      if(dot_pattern[face][dot]==1)
      {
        digitalWrite(pin[dot], HIGH);
      }
      else
      {
        digitalWrite(pin[dot], LOW);
      }
    }
  tone(13,500,10);
  delay(delay_ms);
  delay_ms += 5;
  }
  face= random(6);
   for(int dot=0; dot<7; dot++)
    {
      if(dot_pattern[face][dot]==1)
      {
        digitalWrite(pin[dot], HIGH);
      }
      else
      {
        digitalWrite(pin[dot], LOW);
      }
    }
  
}
  
  
  
void loop()
{
  if(digitalRead(7)==LOW)
  {
    throw_1();
    for(int freq=0; freq<3000; freq+=150)
    {
      tone(13, freq);
      delay(50);
    }
    noTone(13);
  }
}
