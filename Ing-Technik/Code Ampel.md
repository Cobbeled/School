#include <Arduino.h>

int input;

int cycle1[3][3] = {

  {0, 0, 1},

  {0, 1, 1},

  {1, 0, 0},

};

int cycle0[3][3] = {

  {1, 0, 0},

  {0, 1, 0},

  {0, 0, 1},

};

int ampelDef[4][3] = {

  {2, 3, 4},

  {5, 6, 7},

  {10, 11, 12},

  {13, 18, 19},

};

int fampelDef[2][2] = {

  {8, 9},

  {16, 17 },

};

int cycleCall(int type, int side);

int fampelt(int type);

int fampel();

  

void setup() {

  for (size_t i = 0; i < 19; i++)

  {

    pinMode(2+i, OUTPUT);

  }

}

void loop() {

  fampel();

  cycleCall(0, 1);

  cycleCall(1, 0);

  fampelt(0);

  delay(5000);

  fampel();

  cycleCall(0, 0);

  cycleCall(1, 1);

  fampelt(1);

  delay(5000);

}

int fampelt(int type){

      digitalWrite(fampelDef[type][0], 1);

      digitalWrite(fampelDef[type][1], 0);

}

int fampel(){

  for (size_t i = 0; i < 2; i++)

  {

      digitalWrite(fampelDef[i][0], 0);

      digitalWrite(fampelDef[i][1], 1);

    }

  }

int cycleCall(int type, int side){

  for (size_t i = 0; i < 3; i++)

  {

    for (size_t j = 0; j < 3; j++)

    {

      if (type == 1)

      {

        digitalWrite(ampelDef[0+2*side][j], cycle1[i][j]);

        digitalWrite(ampelDef[1+2*side][j], cycle1[i][j]);

      }

      else if (type == 0)

      {

        digitalWrite(ampelDef[0+2*side][j], cycle0[i][j]);

        digitalWrite(ampelDef[1+2*side][j], cycle0[i][j]);

      }

    }

    delay(500);

  }

}

/*int road1(int status, int side);

int roadf(int status, int side);

void setup() {

  for (size_t i = 0; i < 16; i++)

  {

    pinMode(2+i, OUTPUT);

  }

  

  roadf(1, 0);

  roadf(0, 1);

  road1(0, 0);

  road1(0, 1);

  road1(1, 2);

  road1(1, 3);

}

  

void loop() {

  roadf(1, 0);

  delay(1000);

  for (size_t i = 0; i < 2; i++)

  {

    road1(1, i);

    road1(0, (i+2));

  }

  delay(1000);

  roadf(0, 1);

  delay(5000);

  roadf(1, 1);

  delay(1000);

  for (size_t i = 0; i < 2; i++)

  {

    road1(0, i);

    road1(1, (i+2));

  }

  delay(1000);

  roadf(0, 0);

  delay(5000);

  

  

}

  

int road1(int status, int side)

{

  int x;

  int y;

  switch (side)

  {

  case 0:

    x = 0;

    y = 0;

  case 1:

    x = 3;

    y = 0;

  case 2:

    x = 8;

    y = 0;

  case 3:

    x = 11;

    y = 4;

  }

  switch (status)

  {

  case  1:

    digitalWrite(2+x, LOW);

    digitalWrite(3+x+y, HIGH);

    delay(500);

    digitalWrite(3+x+y, LOW);

    digitalWrite(4+x+y, HIGH);

    break;

  case 0:

    digitalWrite(3+x+y, HIGH);

    delay(500);

    digitalWrite(4+x+y, LOW);

    digitalWrite(3+x+y, LOW);

    digitalWrite(2+x, HIGH);

    break;

  default:

    break;

  }

}

int roadf(int status, int side){

  int x;

  switch (side)

  {

  case 0:

    x = 0;

  case 1:

    x = 8;

  }

  switch (status)

  {

  case 1:

    digitalWrite(8+x, LOW);

    digitalWrite(9+x, HIGH);

    break;

  case 0:

    digitalWrite(9+x, LOW);

    digitalWrite(8+x, HIGH);

    break;

  }

}*/