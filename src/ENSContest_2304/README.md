#### 1.- Click en: https://code4rena.com/contests/2023-04-ens-contest

#### 2.- Ir donde pone scope: Aquí están los contratos a vigilar.

2.1.- Con click en cada contrato sale el código de cada uno de ellos.

2.2.- El contrato empieza con la palabra "contract" o "library", lo anterior, no importa.

#### 3.- Vulnerabilidad 1: Las variables

3.1.- Buscar las palabras "uint" - "uint<número>" - "string" - "address" - "bytes"

3.2.- Si están dentro de una función tal que "function(uint aaa) {}" o "function() {uint aaaa}" no se apuntan.

3.3.- Apuntar este contrato y en qué lineas están.

3.4.- Si están agrupadas, la notación normal es tal que "13..21", es decir, hay variables de la 13 a la 21.

#### 4.- Vulnerabilidad 2: emit 

4.1.- Buscar la palabra emit

4.2.- Si, entre los () hay una palabra en mayúsculas, apuntar

4.3.- Ejemplo: "emit(aaa, bbb, CCCC, ddd);"

#### 5.- 


