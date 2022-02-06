# ﻿# TP: Cryptosystème de Vignère
Barazzouk ALi
## Table of content
- Definition
- Objectif
- Chiffrement de Vigenère
- Déchiffrement de Vigenère
- Attaque par force brute
- Conclusion
## Definition
Le chiffre de Vigenère est une méthode de chiffrement par substitution dans laquelle une lettre de l'alphabet est remplacée par un autre symbole selon une clé.
## Objectif 
  L'objectif de ce TP est d'implementer des fonctions pour le chiffrement et le dechiffrement du cryptosysteme de Vigenere et puis initialiser une attaque a force brute.
## Chiffrement de Vigenère
Dans le cryptosystème de Vigenère, on code une lettre avec le décalage de son rang par rapport à la lettre du mot-clé. On répète le mot-clé tout au long du texte. Si on arrive à un rang plus grand que le nombre de lettres dans le mot-clé, on recommence au début. Par exemple si l’alphabet est ABCDEF et que le mot est CLEPENDULA, il faut codifier C par A, L par B, E par C. puis P par D, E par E et ainsi de suite jusqu’à ce qu’on arrive à bout du texte:
```cpp
#include<iostream>
#include<string>
#include<cstring>
#include<algorithm>
#include<bits/stdc++.h>
using namespace std;

int getposition(const char *array, int size, char c)
{
    for (size_t i = 0; i < size; i++)
    {
        if (array[i] == c)
            return (int)i;
    }
    
}
int main() {
   string msg ;
   string key;
   cout << "msg :" << endl;
   getline(cin,msg);
   cout << "key :" << endl;
   getline(cin,key);
   msg.erase(std::remove (msg.begin(), msg.end(), ' '), msg.end());
   transform(msg.begin(), msg.end(), msg.begin(), ::toupper);
   transform(key.begin(), key.end(), key.begin(), ::toupper);

    char alphabet[26]={'A','B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R','S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'};
    char msg_array[msg.length()];
    char key_array[key.length()];
    strcpy(msg_array, msg.c_str());
    strcpy(key_array, key.c_str());
    int outm_array[msg.length()];
    int outk_array[key.length()];
    for(int i=0;i<msg.length();i++)
        outm_array[i]=getposition(alphabet,26,msg_array[i]);
    for(int i=0;i<key.length();i++)
        outk_array[i]=getposition(alphabet,26,key_array[i]);
    int out_array[msg.length()];
    for(int i=0;i<msg.length();i++)
    	out_array[i]=((outm_array[i]+outk_array[(i+1)%key.length()])+26)%26;
	
        
   
	string o_array;
    for(int i=0;i<msg.length();i++)
        o_array+=alphabet[out_array[i]];
    
   cout << msg<<endl;
   cout << o_array;
  return 0;
}
```
## Déchiffrement de Vigenère
Développez l’application du codage de César, et utilisez ce dernier pour construire une fonction Déchiffrer(Ciphertext , Keyword) qui prend en paramètre deux chaines de caractères Ciphertext et Keyword et qui renvoie le texte clair Plaintext.
```cpp
#include<iostream>
#include<string>
#include<cstring>
#include<algorithm>
#include<bits/stdc++.h>
using namespace std;

int getposition(const char *array, int size, char c)
{
    for (size_t i = 0; i < size; i++)
    {
        if (array[i] == c)
            return (int)i;
    }
    
}
int main() {
   string msg ;
   string key;
   cout << "msg a dechiffrer :" << endl;
   getline(cin,msg);
   cout << "key :" << endl;
   getline(cin,key);
   msg.erase(std::remove (msg.begin(), msg.end(), ' '), msg.end());
   transform(msg.begin(), msg.end(), msg.begin(), ::toupper);
   transform(key.begin(), key.end(), key.begin(), ::toupper);

    char alphabet[26]={'A','B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R','S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'};
    char msg_array[msg.length()];
    char key_array[key.length()];
    strcpy(msg_array, msg.c_str());
    strcpy(key_array, key.c_str());
    int outm_array[msg.length()];
    int outk_array[key.length()];
    for(int i=0;i<msg.length();i++)
        outm_array[i]=getposition(alphabet,26,msg_array[i]);
    for(int i=0;i<key.length();i++)
        outk_array[i]=getposition(alphabet,26,key_array[i]);
    int out_array[msg.length()];
    for(int i=0;i<msg.length();i++)
    	out_array[i]=((outm_array[i]-outk_array[(i+1)%key.length()])+26)%26;
	
        
   
	string o_array;
    for(int i=0;i<msg.length();i++)
        o_array+=alphabet[out_array[i]];
    
   cout << msg<<endl;
   cout << o_array;
  return 0;
}
```
## Conclusion
Toujours une fois de plus, le chiffrement de Vigenère s'effectue de la même façon que l'algorithme de chiffrement de cezar, en adaptant à chaque étape la clef utilisée. On peut aussi faire abstraction du mot clef et considérer que celui-ci correspond à une série de nombres unique (caractère => 1, 2, 3, ..).

 
