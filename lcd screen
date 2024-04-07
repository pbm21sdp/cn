#include <LiquidCrystal.h> // libraria LiquidCrystal permite comunicarea cu afisajele cu cristale lichide, permitand unei placi Arduino sa controleze LCD-uri

const int rs = 12; // pin-ul RS de pe LCD este conectat la pinul 12 de pe Arduino
const int en = 11; // pin-ul enable de pe LCD este conectat la pinul 11 de pe Arduino 
const int d7 = 2, d6 = 3, d5 = 4, d4 = 5; // data pins d7, d6, d5, d4 de pe LCD sunt conectati la pinii 2, 3, 4, respectiv 5 de pe Arduino
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);  // creeaza o variabila de tip LCD seteaza pinii pentru conexiunea LCD

void setup() // functie folosita pentru initializare, care va rula o singura data, dupa fiecare pornire sau resetare a placutei Arduino
{
  lcd.begin(16, 2);  // initializeaza LCD-ul cu 16 coloane si 2 linii
  Serial.begin(9600);  // initializeaza comunicarea serială pentru a citi textul
}

void slide(String TextParametru) // primeste ca parametru o variabila de tip String
{   
    lcd.clear(); // goleste/curata ecranul LCD
    unsigned int TextLength = TextParametru.length(); // variabila de tip int care stocheaza lungimea cuvantului dat ca parametru 
  
    for(int i = 0; i < TextLength; i++) // for exterior care se executa pentru fiecare caracter din variabila primita ca parametru
    {
      	if(TextParametru[i] == ' ') continue; // daca un caracter din textul primit ca si parametru este spatiu, trece la iteratia urmatoare pentru a economisi timp
        for(int j = 15; j >= i; j--) // for interior care se executa de 16 - i ori
        { 
            lcd.setCursor(j, 0); // setează cursorul pe poziția curentă (j), pe prima linie (0, linia de sus)
      
            if (j + i < 15 + TextLength) // verifică dacă litera se află pe ecran
            { 
                lcd.print(TextParametru[i]); // afișează litera curentă
            }

            delay(200); // așteaptă pentru efectul de alunecare 200 de ms
            lcd.setCursor(j, 0); // setează cursorul înapoi pe poziția curentă (j), pe primul rand (0, cel de sus)
            lcd.print(" "); // sterge litera curenta
        }

        lcd.setCursor(i, 0); // seteaza cursorul pe cea mai din stanga pozitie (0) si o schimba crescator in functie de i, pentru a insirui literele
        lcd.print(TextParametru[i]); // afiseaza litera cu indexul i din text 
        delay(1000); // așteaptă 1 secundă între fiecare literă
    }
}

void zigzag(String TextParametru) // primeste ca parametru o variabila de tip String
{
    lcd.clear(); // curata ecranul LCD
    unsigned int TextLength = TextParametru.length(); // variabila de tip int care stocheaza lungimea cuvantului dat ca parametru
  
    for (int i = 0; i < TextLength; i++) // for exterior care se executa pentru fiecare litera a cuvantului 
    {
      	if(TextParametru[i] == ' ') continue; // daca un caracter din textul primit ca si parametru este spatiu, trece la iteratia urmatoare pentru a economisi timp
        for (int j = 15; j >= i; j--) // for interior care strabate ecranul de pe cea mai din dreapta pozitie (15, 0), pana in capat sau dupa litera anterioara
        {
            if(i % 2 == 0) // verifica daca se afla la un index par 
            {
                lcd.setCursor(j, j % 2); // daca da, seteaza cursorul la pozitia curenta, pe randul 0/1, in functie de litera
        
                if(j + i < 15 + TextLength) // verifica daca litera se afla pe ecran
                {
        	          lcd.print(TextParametru[i]); // afiseaza caracterul curent
                }

      	        delay(200); // asteapta 200 de milisecunde 
   	  	        lcd.setCursor(j, j % 2); // se intoarce la litera curenta dupa ce a afisat-o
      	        lcd.print(" "); // sterge litera afisata anterior
            }
            else
            {
                lcd.setCursor(j, (j + 1) % 2); // daca indexul este impar, seteaza cursorul tot pe randul 0/1, in  functie de litera
        
                if(j + i < 15 + TextLength) // verifica daca litera se afla pe ecran 
                {
        	          lcd.print(TextParametru[i]); // afiseaza caracterul curent
                }
        
      	        delay(200); // asteapta 200 de milisecunde
   	  	        lcd.setCursor(j, (j +1) % 2); // se intoarce la litera curenta dupa ce a afisat-o
      	        lcd.print(" "); // sterge litera afisata anterior
            }
        }

        lcd.setCursor(i, 0); // seteaza cursorul pe cea mai din stanga pozitie (0) si o schimba crescator in functie de i, pentru a insirui literele
        lcd.print(TextParametru[i]); // afiseaza litera cu indexul i din text
        delay(1000); // asteapta 1 secunda intre fiecare litera
    }
    lcd.clear(); // curata/goleste ecranul LCD
}

void moving_text(String TextParametru) // primeste ca parametru o variabila de tip String 
{
    unsigned int TextLength = TextParametru.length(); // variabila de tip int care stocheaza lungimea cuvantului dat ca parametru
    unsigned int RepeatCount = 0; // contor care asigura repetitia functiei de un numar stabilit de ori

  	while (RepeatCount < 3) // bucla pentru a executa functia de un numar stabilit de ori
    {
      	for (int i = 0; ; i++) // for care sa ruleze fara conditie de oprire, pentru ca "oprirea" este data de % din index
        {
            int index = i % (TextLength + 16); // variabila de tip int care va fi utilizata pentru a determina pozitia textului pe ecran 
          	lcd.clear(); // curata ecranul LCD
          
          	if (15 - index < 0) // verifica daca a ajuns textul in capat (a parcurs mai mult de 15 pozitii)
            {
            	lcd.setCursor(0, 0); // daca a depasit, se seteaza cursorul pe cea mai din stanga pozitie 
            	lcd.print(TextParametru.substring(index - 15)); // se afiseaza portiunea din text care a ramas pe ecran dupa ce restul "a disparut" in stanga
          	} 
            else // daca inca nu a fost parcurs tot ecranul
            {
            	lcd.setCursor(15 - index, 0); // se deplaseaza cursorul succesiv spre stanga
            	lcd.print(TextParametru); // se afiseaza intreg cuvantul, cu text[0] fiind pe pozitia setata de cursor anterior
          	}

          	delay(300); // asteapta 300 de milisecunde 
          
            RepeatCount++; // se incrementeaza contorul care stocheaza numarul de iteratii dorite 
            if(RepeatCount == 3 * (TextLength + 16)) // daca s-a ajuns la numarul dorit, executia se incheie 
            {
              break; // intrerupe executia buclei interioare 
            }
        }
    }
}

void middle(String TextParametru) // primeste ca parametru o variabila de tip String
{
    int TextLength = TextParametru.length(); // variabila de tip int care stocheaza lungimea cuvantului dat ca parametru 
    unsigned int LeftPosition = 7; // seteaza indexul initial din stanga pe 7 (partea stanga a mijlocului ecranului)
    unsigned int RightPosition = 8; // seteaza indexul initial din dreapta pe 8 (partea dreapta a mijlocului ecranului)
  
    for(int i = 0; i < TextLength - 2; i++) // bucla care se executa pentru toate caracterele parametrului, mai putin cele 2 care deja au index
    {
        if((TextLength / 2 - 1 - i) < 0 && (TextLength / 2 + i) >= TextLength) // verifica daca mai exista caractere in stanga si in dreapta mijlocului
        {
            break; // opreste executia 
        }

        if(LeftPosition >= 0 && (TextLength / 2 - 1 - i) >= 0) // verifica daca inca mai exista pozitii in stanga si daca mai sunt caractere de afisat 
        {
            lcd.setCursor(LeftPosition, 0); // deplaseaza cursorul pe randul 0, pana la pozitia indicata de LeftPosition
            lcd.print(TextParametru[TextLength / 2 - 1 - i]); // afiseaza caracterul care corespunde acelei pozitii
        }
    
        delay(300); // asteapta 300 de milisecunde
        LeftPosition--; // actualizeaza pozitia stanga, decrementand variabila LeftPosition

        if(RightPosition < 16 && (TextLength / 2 + i) < TextLength) // verifica daca inca mai exista pozitii in dreapta si daca mai sunt caractere de afisat
        { 
            lcd.setCursor(RightPosition, 0); // deplaseaza cursorul pe randul 0, pana la pozitia indicata de RightPosition
            lcd.print(TextParametru[TextLength / 2 + i]); // afiseaza caracterul care corespunde acelei pozitii
        }
  
        delay(300); // asteapta 300 de milisecunde 
        RightPosition++; // actualizeaza pozitia dreapta, incrementand variabila RightPosition
    }
  
    for(int i = 0; i < 3; i++) // bucla care se executa de 3 ori pentru a asigura efectul de ”blink”
    {
        lcd.clear(); // curata ecranul LCD 
        delay(1000); // asteapta 1 secunda 
      
      	if(TextLength % 2 == 1) // verifica daca parametrul are nr impar de caractere
        {
        	lcd.setCursor(LeftPosition + 2, 0); // pozitioneaza cursorul la valoarea finala a lui LeftPosition, la care se aduna 2, pe randul 0
        }
      	else // daca parametrul are nr par de caractere
        {
          lcd.setCursor(LeftPosition + 1, 0); // pozitioneaza cursorul la valoarea finala a lui LeftPosition, la care se aduna 1, pe randul 0
        }
      
      	lcd.print(TextParametru); // afiseaza intreg textul primit ca parametru
        delay(1000); // asteapta o secunda 
    }
  
    lcd.clear(); // curata ecranul LCD 
    delay(1000); // asteapta o secunda
  
  	if(TextLength % 2 == 1) // verifica daca parametrul are nr impar de caractere
    {
        lcd.setCursor(LeftPosition + 2, 0); // pozitioneaza cursorul la valoarea finala a lui LeftPosition, la care se aduna 2, pe randul 0
    }
    else // daca parametrul are nr par de caractere
    {
        lcd.setCursor(LeftPosition + 1, 0); // pozitioneaza cursorul la valoarea finala a lui LeftPosition, la care se aduna 1, pe randul 0
    }
  
    lcd.print(TextParametru); // Afiseaza intreg textul primit ca parametru
    delay(1000); // asteapta o secunda
}

void loop() // se executa la infinit
{
  	if (Serial.available() > 0) // verifica daca numarul de bytes disponibili pentru citire de la monitorul serial este mai mare decat 0
  	{
    	String TextInput; // variabila de tip String care va stoca textul provenit de la monitorul serial
    	TextInput = Serial.readString(); // i se atribuie variabilei TextInput continutul provenit de la monitorul serial
    
   		slide(TextInput); // se apeleaza functia slide 
    	delay(1000); // o pauza de 1 secundă între animații
      
    	zigzag(TextInput); // se apeleaza functia zigzag
    	delay(1000); // o pauza de 1 secundă între animații
      
    	moving_text(TextInput); // se apeleaza functia moving_text
    	delay(1000); // o pauza de 1 secundă între animații
      
    	middle(TextInput); // se apeleaza functia middle 
    	delay(3000); // o pauza de 3 secunde între animații
      
      	lcd.clear(); // curata ecranul LCD
  	}
}
