# Curso de Programación en Bash Shell

URL: https://platzi.com/cursos/bash-shell/ 

## Slides del curso

[Slides Bash shell](src/shell.pdf)

## ****Componentes de Linux, Tipos de Shell y Comandos de información****

Linux tiene 3 partes principales:

- **Kernel**: Es el núcleo del Sistema Operativo y se gestionan los recursos de hardware como la memoria, el procesamiento y los dispositivos periféricos conectados al computador.
- **Shell**: Es el interprete, un programa con una interfaz de usuario permitiendo ejecutar las aplicaciones en un lenguaje de alto nivel y procesarlas en un lenguaje de bajo nivel para manipular y controlar aplicaciones y programas como nuestro proyecto.
- Aplicaciones: Son las aplicaciones con las que interactuamos día a día.

Tipos de Shells:

- SH
- KSH
- CSH
- BASH

Algunos comandos para conocer información sobre el resto de comandos:

- `man [comando]`
- `info [comando]`

## ****Bash scripting****

La idea básica de generar programas en bash es poder ejecutar múltiples comandos de forma secuencial en muchas ocasiones para automatizar una tarea en especifico. Estos comandos son colocados en un archivo de textos de manera secuencial para poder ejecutarlos a posterioridad.

Un archivo `.vimrc` podremos configurar de mejor manera nuestro editor VIM.

Presionamos `I` para poder escribir en nuestro editor.Presionamos `ESC` para salir del modo edición, luego escribimos `:wq` para salir y guardar nuestro archivo.

## Operadores

Por si alguien olvido los operadores:

- gt mayor
- lt menor
- ge mayor o igual
- le menor o igual
- eq igual
- ne distinto

Otros operadores [https://www.atareao.es/tutorial/scripts-en-bash/condicionales-en-bash/#](https://www.atareao.es/tutorial/scripts-en-bash/condicionales-en-bash/#)

## ****Crear nuestro primer Script****

```bash
# !/bin/bash
# Programa para realizar algunas operaciones utilitarios de Postgres

echo "Hola bienvenido al curso de Programación bash"
```

```bash
#! /bin/bash
# PROGRAMA: U-POSG
echo "Programa Utilidades Postgres"
    <<"COMENTARIO 1"
    Programa para administrar las utilidades de la Base
    de Datos Postgres
   "COMENTARIO 1"
    
exit 0
```

## ****Declaración de Variables y Alcance en Bash Shell****

**1 Variables de entorno**Ayudan a obtener infromacion del sistema, almacenar informacion temporal y modificar su informacion. Existen 2 tipos:

*Variables Globales:* Son visibles desde el shell que lo creo o desde cuaquier hijo de esa shell.

*Variables Locales:* Son visibles solo desde el shell que la creo.

*Variable Persistente:* Para crear una de estas es necesario introducirla en el archivo /etc/profile pero en el caso de los derivados debian si revisamos un poco el script nos damos cuenta que llama a otro archivo llamado /etc/bash.bashrc en el cual podemos crear las variables de entorno persistentes.

*Por eso no funciona llamar la variable declarada en /etc/profile desde un shell*

**2 Variables de usuario**Son las variables que se corren dentro de un script como en cualquier programa de computadora C, C++ o Java

*Variable global:* Se puede usar desde otro script siempre y cuando sea llamado desde el script que contiene la variable.

- Variable local:_ Solo tiene alcance en el script que la creo.

```bash
# !/bin/bash
# Programa para revisar la declaración de variables
# Autor: Marco Toscano Freire - @martosfre

opcion=0
nombre=Marco

echo "Opción: $opcion y Nombre: $nombre"

# Exportar la variable nombre para que este disponible a los demÃ¡s procesos
export nombre

# Llamar al siguiente script para recuperar la variable
./2_variables_2.sh
```

```bash
# !/bin/bash
# Programa para revisar la declaración de variables
# Autor: Marco Toscano Freire - @martosfre

echo "Opción nombre pasada del script anterior: $nombre"
```

## ****Tipos de Operadores****

```bash
# ! /bin/bash
# Programa para revisar los tipos de operadores
# Autor: Marco Toscano - @martosfre

numA=10
numB=4

echo "Operadores Aritméticos"
echo "Números: A=$numA y B=$numB"
echo "Sumar A + B =" $((numA + numB))
echo "Restar A - B =" $((numA - numB))
echo "Multiplicar A * B =" $((numA * numB))
echo "Dividir A / B =" $((numA / numB))
echo "Residuo A % B =" $((numA % numB))

echo -e "\nOperadores Relaciones"
echo "Números: A=$numA y B=$numB"
echo "A > B =" $((numA > numB))
echo "A < B =" $((numA < numB))
echo "A >= B =" $((numA >= numB))
echo "A <= B =" $((numA <= numB))
echo "A == B =" $((numA == numB))
echo "A != B =" $((numA != numB))

echo -e "\nOperadores Asignación"
echo "Números: A=$numA y B=$numB"
echo "Sumar A += B" $((numA += numB))
echo "Restar A -= B" $((numA -= numB))
echo "Multiplicación A *= B" $((numA *= numB))
echo "Dividir A /= B" $((numA /= numB))
echo "Residuo A %= B" $((numA %= numB))
```

## ****Script con Argumentos****

Hay algunos identificadores para cuando ejecutamos un script con argumentos

**$0**: Se refiere al nombre del Script**$1 al ${10}**: Se refiere al número de argumento. Si es más de uno lo colocamos dentro de llaves.**$#**: Es útil para conocer el número de argumentos enviados.**$***: Con este podemos conocer todos los argumentos enviados.

```bash
# ! /bin/bash
# Programa para ejemplificar el paso de argumentos
# Autor: Marco Toscano Freire - @martosfre

nombreCurso=$1
horarioCurso=$2

echo "El nombre del curso es: $nombreCurso dictado en el horario de $horarioCurso"
echo "El número de parÃ¡metros enviados es: $#"
echo "Los parÃ¡metros enviados son: $*"
```

## ****Sustitución de Comandos en variables****

Para la sustitución de comandos es importante tener en cuenta que el resultado servirá para realizar otras tareas de otras sentencias de nuestro programa.

Las dos maneras de hacerlo:

- Usando el backtick caracter. (`)
- Usando el signo de dólar con el formato $(comando)

```bash
# ! /bin/bash
# Programa para revisar como ejecutar comados dentro de un programa y almacenar en una variable para su posterior utilización
# Autor: Marco Toscano Freire - @martosfre

ubicacionActual=`pwd`
infoKernel=$(uname -a)

echo "La ubicación actual es la siguiente: $ubicacionActual"
echo "Información del Kernel: $infoKernel"
```

## ****Debug en Script****

Para realizar debugging en un script tenemos dos opciones en el comando de bash:

- **v**: Utilizado para ver el resultado detallado de nuestro script, evaluado línea por línea.
- **x**: Utilizado para desplegar la información de los comandos que son usados, capturando el comando y su salida.

## Reto 1

```bash
#! /bin/bash

option=$1
result=$2

echo -e "option= $1\n"
echo "result= $2"
```

## ****Capturar información usuario****

Para poder capturar información tenemos dos formas dentro de un programa Bash.

- Utilizando en conjunto con el comando **echo**
- Utilizando directamente el comando **read**

```bash
# ! /bin/bash
# Programa para ejemplificar como capturar la información del usuario utilizando el comando echo, read y $REPLY
# Autor: Marco Toscano Freire - @martosfre

option=0
backupName=""

echo "Programa Utilidades Postgres"
echo -n "Ingresar una opción:"
read
option=$REPLY
echo -n "Ingresar el nombre del archivo del backup:"
read
backupName=$REPLY
echo "Opción:$option , backupName:$backupName"
```

```bash
# ! /bin/bash
# Programa para ejemplificar como capturar la información del usuario utilizando el comando read
# Autor: Marco Toscano Freire - @martosfre

option=0
backupName=""

echo "Programa Utilidades Postgres"
read -p "Ingresar una opción:" option
read -p "Ingresar el nombre del archivo del backup:" backupName
echo "Opción:$option , backupName:$backupName"
```

## ****Expresiones Regulares****

Cuando se solicita ingresar información través de un programa por parte del usuario que está utilizando el programa, independientemente el lenguaje que esté realizado; es importante considerar la validación de la información no solo en su tamaño sino también en los tipos de datos, formatos soportados lo cual nos permite asegurar la calidad de la información que recibimos, almacenamos y procesamos.

Dentro de este contexto en la programación bash para cumplir con este objetivo se utiliza expresiones regulares, las cuales son básicamente cadenas de caracteres que definen un patrón de búsqueda que se valida frente a una información específica para asegurar que cumple la validación definida.

Se necesita conocer ciertos criterios utilizados en las expresiones regulares que son los siguientes:

- ^.- Caracter que representa el inicio de la expresión regular.
- $.- Caracter que representa el final de la expresión regular.
- .- Caracter que representa cero o más ocurrencias de la expresión
- +.- Caracter que representa una o más ocurrencias de la expresión.
- {n}.-Representa n veces de una expresión.
- [ ]  .- Representa un conjunto de caracteres, por ejemplo: [a-z] representa las letras del abecedario de la a a la z.

Tomando en cuenta estos criterios se realizará un programa que valida la siguiente información:Número de Identificación de un tamaño de 10 números. Ejemplo: 1717836520País de Origen denotado por dos letras en un rango específico. Ejemplo: EC, CO, USFecha de Nacimiento en el formato yyyyMMDD. Ejemplo: 20181222

Primero se definirá las expresiones regulares y se solicitará la información del usuario:

![https://static.platzi.com/media/user_upload/Captura%20de%20pantalla%202019-01-16%20a%20la%28s%29%2015.58.48-4bedb3f4-a096-4381-97ad-61e73844d1d4.jpg](https://static.platzi.com/media/user_upload/Captura%20de%20pantalla%202019-01-16%20a%20la%28s%29%2015.58.48-4bedb3f4-a096-4381-97ad-61e73844d1d4.jpg)

Luego se validará cada expresión regular comenzando con la identificación, para lo cual para cada validación se utilizará la sentencia condicional if y para comparar la expresión se debe utilizar el siguiente formato especial if [[ $variable =~ $expresionRegular ]] como se muestra a continuación.

![https://static.platzi.com/media/user_upload/Captura%20de%20pantalla%202019-01-16%20a%20la%28s%29%2015.59.26-00ffab79-1f96-4d00-b135-4e82996e1c07.jpg](https://static.platzi.com/media/user_upload/Captura%20de%20pantalla%202019-01-16%20a%20la%28s%29%2015.59.26-00ffab79-1f96-4d00-b135-4e82996e1c07.jpg)

Se realizará la ejecución de la aplicación con los dos escenarios el correcto y el incorrecto como se muestra a continuación:

![https://static.platzi.com/media/user_upload/Captura%20de%20pantalla%202019-01-16%20a%20la%28s%29%2015.59.55-0c3eb175-30c5-4563-97f0-d325ead87735.jpg](https://static.platzi.com/media/user_upload/Captura%20de%20pantalla%202019-01-16%20a%20la%28s%29%2015.59.55-0c3eb175-30c5-4563-97f0-d325ead87735.jpg)

Finalmente el código fuente lo pueden encontrar en el repositorio de GitHub en el branch 7.ValidarInformacion

```bash
# ! /bin/bash
# Programa para ejemplificar como capturar la información del usuario y validarla utilizando expresiones regulares
# Autor: Marco Toscano Freire - @martosfre

identificacionRegex='^[0-9]{10}$'
paisRegex='^EC|COL|US$'
fechaNacimientoRegex='^19|20[0-8]{2}[1-12][1-31]$'

echo "Expresiones regulares"
read -p "Ingresar una identificacion:" identificacion
read -p "Ingresar las iniciales de un paÃ­s [EC, COL, US]:" pais
read -p "Ingresar la fecha de nacimiento [yyyyMMdd]:" fechaNacimiento 

#Validación Identificación
if [[ $identificacion =~ $identificacionRegex ]]; then
    echo "Identificación $identificacion vÃ¡lida"
else
    echo "Identificación $identificacion invÃ¡lida"
fi

#Validación PaÃ­s
if [[ $pais =~ $paisRegex ]]; then
    echo "PaÃ­s $pais vÃ¡lido"
else
    echo "PaÃ­s $pais invÃ¡lido"
fi

#Validación Fecha Nacimiento
if [[ $fechaNacimiento =~ $fechaNacimientoRegex ]]; then
    echo "Fecha Nacimiento $fechaNacimiento vÃ¡lida"
else
    echo "Fecha Nacimiento $fechaNacimiento invÃ¡lida"
fi
```

## ****Validar información****

Para el proceso de validación de información tenemos dos maneras de hacerlo:

- Para validar tamaños se utiliza el siguiente comando: **read -n <numero_caracteres>**
- Para validar el tipo de datos se utilizan las **expresiones regulares**

```bash
# ! /bin/bash
# Programa para ejemplificar como capturar la información del usuario y validarla
# Autor: Marco Toscano Freire - @martosfre

option=0
backupName=""
clave=""

echo "Programa Utilidades Postgres"
# Acepta el ingreso de información de solo un caracter
read -n1 -p "Ingresar una opción:" option
echo -e "\n"
read -n10 -p "Ingresar el nombre del archivo del backup:" backupName
echo -e "\n"
echo "Opción:$option , backupName:$backupName"
read -s -p "Clave:" clave
echo "Clave: $clave"
```

## ****Paso de parámetros y opciones****

```bash
# ! /bin/bash
# Programa para ejemplificar como se realiza el paso de opciones con sin parÃ¡metros
# Autor: Marco Toscano - @martosfre

echo "Programa Opciones"
echo "Opción 1 enviada: $1"
echo "Opción 2 enviada: $2"
echo "Opción enviadas: $*"
echo -e "\n"
echo "Recuperar valores"
while [ -n "$1" ]
do
case "$1" in
-a) echo "-a option utilizada";;
-b) echo "-b option utilizada";;
-c) echo "-c option utlizada";;
*) echo "$! no es una opción";;
esac
shift
done
```

## ****Descargar información de Internet****

```bash
# !/bin/bash
# Programa para ejemplificar el uso de la descarga de información desde internet utilizando el comando wget
# Autor: Marco Toscano Freire - @martosfre

echo "Descargar información de internet"
wget https://www-us.apache.org/dist/tomcat/tomcat-8/v8.5.35/bin/apache-tomcat-8.5.35.zip
```

## Reto 2

```bash
#!/bin/bash

regexedad='^([1-9]{1,2})$'
regexnombre='^([A-z]{2,})$'
regexapellido='^([A-z]{2,})$'
regexdireccion='^([A-Z]*)'
regexnumero='^[0-9]{10})$'

read -p "Ingrese su nombre: " nombre
read -p "Ingrese su Apellido: " apellido
read -p "Ingrese su edad: " edad
read -p "ingrese su dirección: " direccion
read -p "ingrese su numero de telefono: " telefono

if [[ $edad =~ $regexedad ]]; then
	echo "edad valida"
else
	echo "edad invalida"
fi

if [[ $nombre =~ $regexnombre ]]; then
	echo "nombre valido"
else
	echo "nombre invalido"
fi

if [[ $apellido =~ $regexapellido ]]; then
	echo "apellido valido"
else
	echo "apellido invalido"
fi

if [[ $direccion =~ $regexdireccion ]]; then
	echo "Dirección valida"
else
	echo "Dirección invalida"
fi

if [[ $telefono =~ $regextelefono ]]; then
	echo "telefono valido"
else
	echo "telefono invalido"
fi

echo "los datos"
echo $nombre
echo $apellido
echo $edad
echo $direccion
echo $telefono
```

## ****Sentencias If/Else****

```bash
# !/bin/bash
# Programa para ejemplificar el uso de la sentencia de decisión if, else if, else
# Autor: Marco Toscano Freire - @martosfre

edad=0

echo "Ejemplo Sentencia If -else"
read -p "Indique cúal es su edad:" edad
if [ $edad -le 18 ]; then
    echo "La persona es adolescente"
elif [ $edad -ge 19 ] && [ $edad -le 64 ]; then
    echo "La persona es adulta"
else
    echo "La persona es adulto mayor"
fi
```

## Reto 3

```bash
#! /bin/bash
#Reto 3
#Autor Jose Suarez

read -p "Ingrese su nombre: " nombre

echo -e "\n Bienvenido $nombre \n"
echo "+++++++++++++++++++++++++++++++"
echo "     Reto al conocimiento"
echo -e "+++++++++++++++++++++++++++++++\n"

echo "1.- Matematica"
echo "2.- Deportes"
echo "3.- Historia"
echo "4.- Arte"
echo "5.- Geografia"
echo -e "\n++++++++++++++++++++++++++++++++\n"                                                          
read -n1 -p "Ingrese su opcion: " opcion                                                                
echo -e "\n"                                                                                                                                                                                                    case $opcion in
1) read -p " ¿Cual es la raiz cuadrada de 16? " respmat                                                         
if [ $respmat = "4" ]; then                                                                                 
echo "Correcto, la raiz cuadrada de 16 es 4"                                                        
else                                                                                                        
echo "Respuesta incorrecta, la raiz cuadrada de 16 no es $respmat"                                  fi;;  
                                                                                                                                                                                                  2) read -p " ¿Que organismo que gobierna las federaciones de fútbol en todo el mundo? " respdep                 
if [ $respdep = "fifa" ] || [ $respdep = "FIFA" ] || [ $respdep = "Fifa" ] ; then                           
echo "Correcto, la FIFA"                                                                            
else                                                                                                        
echo "Respuesta incorrecta, no es $respdep"                                                         
fi;;
                                                                                                                                                                                                    3) read -p " ¿Cual es el apellido del Libertador de América? " resphis                                          
if [ $resphis = "Bolivar" ] || [ $resphis = "BOLIVAR" ] || [ $resphis = "bolivar" ]; then                       
echo "Correcto, el Libertador de América es Simón Bolivar"                                          
else                                                                                                        
echo "Respuesta incorrecta, el apellido del Libertador no es $resphis"                              fi;;        

4) read -p " ¿En qué año nació el Pintor Italiano Leonardo da Vinci? " respart
if [ $respart = "1452" ]; then
                echo "Correcto, Leonardo da Vinci nació en el 1452 y murió en el año 1519"
 else
                echo "Respuesta incorrecta, Leonardo da Vinci no nacio en el año $respart"
  fi;;

5) read -p " ¿Cual es la capital de Austria? " respgeo
            if [ $respgeo = "Viena" ] || [ $respgeo = "VIENA" ] || [ $respgeo = "viena" ]; then
                echo "Correcto, la capital de Austria es Viena"
            else
                echo "Respuesta incorrecta, $respgeo no es la capital de Austria"
            fi;;
 esac
```

***OPERADORES RELACIONALES***

- eq: is equal to // Igual a
- ne: is not equal to // No es igual a
- gt: is greater than // Mayor a
- ge: is greater than or equal to // Mayor o igual a
- lt: is less than // Menor a
- le: is less than or equal to // Menor o igual a

## ****If Anidados****

```bash
# !/bin/bash
# Programa para ejemplificar el uso de los ifs anidados
# Autor: Marco Toscano Freire - @martosfre

notaClase=0
continua=""

echo "Ejemplo Sentencia If -else"
read -n1 -p "Indique cúal es su nota (1-9):" notaClase
echo -e "\n"
if [ $notaClase -ge 7 ]; then
    echo "El alumno aprueba la materia"
    read -p "Si va continuar estudiando en el siguiente nivel (s/n):" continua
    if [ $continua = "s" ]; then
        echo "Bienvenido al siguiente nivel"
    else
        echo "Gracias por trabajar con nosotros, mucha suerte !!!"
    fi    
else
    echo "El alumno reprueba la materia"
fi
```

## ****Expresiones Condicionales****

Las expresiones condicionales ya las hemos visto en clases anteriores, pero en qué corresponde y cómo se forman las veremos en esta clase. Estás son las siguientes

- Utilizada en decisión, iteración.
- Formada por una o más condiciones
- Condiciones con tipos de datos diferentes
- Utiliza los operadores relacionales y condicionales

```bash
# !/bin/bash
# Programa para ejemplificar el uso de expresiones condicionales
# Autor: Marco Toscano Freire - @martosfre

edad=0
pais=""
pathArchivo=""

read -p "Ingrese su edad:" edad
read -p "Ingrese su paÃ­s:" pais
read -p "Ingrese el path de su archivo:" pathArchivo

echo -e "\nExpresiones Condicionales con números"
if [ $edad -lt 10 ]; then
    echo "La persona es un niño o niña"
elif [ $edad -ge 10 ] && [ $edad -le 17 ]; then
    echo "La persona se trata de un adolescente"
else
    echo "La persona es mayor de edad"
fi

echo -e "\nExpresiones Condicionales con cadenas"
if [ $pais = "EEUU" ]; then
    echo "La persona es Americana"
elif [ $pais = "Ecuador" ] || [ $pais = "Colombia" ]; then
    echo "La persona es del Sur de América"
else
    echo "Se desconoce la nacionalidad"
fi

echo -e "\nExpresiones Condicionales con archivos"
if [ -d $pathArchivo ]; then
    echo "El directorio $pathArchivo existe"
else 
    echo "El directorio $pathArchivo no existe"
fi
```

## ****Sentencias Case****

En la sentencia Case el objetivo principal es validar una expresión simple, puede ser un número, una cadena o un rango de valores

```bash
# !/bin/bash
# Programa para ejemplificar el uso de la sentencia case
# Autor: Marco Toscano Freire - @martosfre

opcion=""

echo "Ejemplo Sentencia Case"
read -p "Ingrese una opción de la A - Z:" opcion
echo -e "\n"

case $opcion in
    "A") echo -e "\nOperación Guardar Arhivo";;
    "B") echo "Operación Eliminar Archivo";;
    [C-E]) echo "No esta implementada la operación";;
    "*") "Opción Incorrecta"
esac

```

## ****Arreglos****

Los Arreglos son un tipo de variables que puede contener N cantidad de valores ya sean cadenas de texto, numéricos, etc. Estos siempre empiezan desde la posición número 0.

```bash
# ! /bin/bash
# Programa para ejemplificar el uso de los arreglos
# Autor: Marco Toscano Freire - @martosfre

arregloNumeros=(1 2 3 4 5 6)
arregloCadenas=(Marco, Antonio, Pedro, Susana)
arregloRangos=({A..Z} {10..20})

#Imprimir todos los valores
echo "Arreglo de Números:${arregloNumeros[*]}"
echo "Arreglo de Cadenas:${arregloCadenas[*]}"
echo "Arreglo de Números:${arregloRangos[*]}"

#Imprimir los tamaños de los arreglos
echo "Tamaño Arreglo de Números:${#arregloNumeros[*]}"
echo "Tamaño Arreglo de Cadenas:${#arregloCadenas[*]}"
echo "Tamaño Arreglo de Números:${#arregloRangos[*]}"

#Imprimir la posición 3 del arreglo de números, cadenas de rango
echo "Posición 3 Arreglo de Números:${arregloNumeros[3]}"
echo "Posición 3 Arreglo de Cadenas:${arregloCadenas[3]}"
echo "Posición 3 Arreglo de Rangos:${arregloRangos[3]}"

#Añadir y eliminar valores en un arreglo
arregloNumeros[7]=20
unset arregloNumeros[0]
echo "Arreglo de Números:${arregloNumeros[*]}"
echo "Tamaño arreglo de Números:${#arregloNumeros[*]}"
```

## ****Sentencia for loop****

La sentencia For es esa que se suele utilizar mucho cuando se quiere recorrer o iterar sobre una lista de valores. En Bash también soporta el For loop expression el cual tiene tres bloques, tanto de inicialización, condición e iteración.

```bash
# ! /bin/bash
# Programa para ejemplificar el uso de la sentencia de iteración for
# Autor: Marco Toscano Freire - @martosfre

arregloNumeros=(1 2 3 4 5 6)

echo "Iterar en la Lista de Números"
for num in ${arregloNumeros[*]}
do
    echo "Número:$num"
done

echo "Iterar en la lista de Cadenas"
for nom in "Marco" "Pedro" "Luis" "Daniela"
do
    echo "Nombres:$nom"
done

echo "Iterar en Archivos"
for fil in *
do
    echo "Nombre archivo:$fil"
done

echo "Iterar utilizando un comando"
for fil in $(ls)
do
    echo "Nombre archivo:$fil"
done

echo "Iterar utilizando el formato tradcional"
for ((i=1; i<10; i++))
do
    echo "Número;$i"
done
```

## ****Sentencia while loop****

El While itera una lista de valores basada en una condición lógica mientras esta sea verdadera.

```bash
# ! /bin/bash
# Programa para ejemplificar el uso de la sentencia de iteración while
# Autor: Marco Toscano Freire - @martosfre

numero=1

while [ $numero -ne 10 ]
do
    echo "Imprimiendo $numero veces"
    numero=$(( numero + 1 ))
done
```

## ****Loop Anidados****

```bash
# ! /bin/bash
# Programa para ejemplificar el uso de los loops anidados
# Autor: Marco Toscano Freire - @martosfre

echo "Loops Anidados"
for fil in $(ls)
do
    for nombre in {1..4}
    do
        echo "Nombre archivo:$fil _ $nombre"
    done
done
```

## ****Break y continue****

- Break se utiliza para salir de la ejecución de los ciclos for y while.
- Continue se utiliza para continuar con la siguiente ejecución.

```bash
# ! /bin/bash
# Programa para ejemplificar el uso de break y continue
# Autor: Marco Toscano Freire - @martosfre

echo "Sentencias break y continue"
for fil in $(ls)
do
    for nombre in {1..4}
    do
        if [ $fil = "10_download.sh" ]; then
            break;
        elif [[ $fil == 4* ]]; then
            continue;
        else
            echo "Nombre archivo:$fil _ $nombre"
        fi
    done
done
```

## ****Menú de Opciones****

```bash
# ! /bin/bash
# Programa que permite manejar las utilidades de Postres
# Autor: Marco Toscano Freire - @martosfre

opcion=0

while :
do
    #Limpiar la pantalla
    clear
    #Desplegar el menú de opciones
    echo "_________________________________________"
    echo "PGUTIL - Programa de Utilidad de Postgres"
    echo "_________________________________________"
    echo "                MENÚ PRINCIPAL           "
    echo "_________________________________________"
    echo "1. Instalar Postgres"
    echo "2. Desinstalar Postgres"
    echo "3. Sacar un respaldo"
    echo "4. Restar respaldo"
    echo "5. Salir"

    #Leer los datos del usuario - capturar información
    read -n1 -p "Ingrese una opción [1-5]:" opcion

    #Validar la opción ingresada
    case $opcion in
        1)
            echo -e "\nInstalar postgres....."
            sleep 3
            ;;
        2)
            echo -e "\nDesinstalar postgres...."
            sleep 3
            ;;
        3)
            echo -e "\nSacar respaldo..."
            sleep 3
            ;;
        4)
            echo -e "\nRestaurar respaldo..."
            sleep 3
            ;;
        5)
            echo "Salir del Programa"
            exit 0
            ;;
    esac
done
```

## Reto 4:

Crear un menú con las siguientes opciones:

1. Procesos Actuales,
2. Memoria Disponible,
3. Espacio en Disco,
4. Información de Red,
5. Variables de Entorno Configuradas,
6. Información Programa
7. Backup información
8. Ingrese una opción.

Posterior a esto vamos  a recuperar la opción ingresada, validarla e imprimir la opción y el título de acuerdo a lo ingresado

## ****Archivos y Directorios****

- Para crear directorios utilizamos el comando **mkdir** seguido del nombre que queremos colocar.
- Para crear archivos utilizamos el comando **touch** seguido del nombre que queremos colocar.

```bash
# ! /bin/bash
# Programa para ejemplificar la creación de archivos y directorios
# Autor: Marco Toscano Freire - @martosfre

echo "Archivos - Directorios"

if [ $1 = "d" ]; then
    mkdir -m 755 $2
    echo "Directorio creado correctamente"
    ls -la $2
elif [ $1 == "f" ]; then
    touch $2
    echo "Archivo creado correctamente"
    ls -la $2
else
    echo "No existe esa opción: $1"
 fi
```

## ****Escribir dentro de archivos****

```bash
# ! /bin/bash
# Programa para ejemplificar como se escribe en un archivo
# Autor: Marco Toscano Freire - @martosfre

echo "Escribir en un archivo"

echo "Valores escritos con el comando echo" >> $1

#Adición multilínea
cat <<EOM >>$1
$2
EOM
```

## Leer archivos

```bash
# ! /bin/bash
# Programa para ejemplificar como se lee en un archivo
# Autor: Marco Toscano Freire - @martosfre

echo "Leer en un archivo"
cat $1
echo -e "\nAlmacenar los valores en una variable"
valorCat=`cat $1`
echo "$valorCat"

# Se utiliza la variable IFS (Internal Field Separator) para evitar que los espacios en blanco al inicio al final se recortan
echo -e "\nLeer archivos lÃ­nea por lÃ­nea utilizando while"
while IFS= read linea
do
    echo "$linea"
done < $1
```

## Operaciones Archivo

```bash
# ! /bin/bash
# Programa para ejemplificar las operaciones de un archivo
# Autor: Marco Toscano Freire - @martosfre

echo "Operaciones de un archivo"
mkdir -m 755 backupScripts

echo -e "\nCopiar los scripts del directorio actual al nuevo directorio backupScripts"
cp *.* backupScripts/
ls -la backupScripts/

echo -e "\nMover el directorio backupScripts a otra ubicación: $HOME"
mv backupScripts $HOME

echo -e "\nEliminar los archivos .txt"
rm *.txt
```

## Reto 5

```bash
# !/bin/bash
# Reto 5. Generar un archivo log, escribir dentro de este archivo el usuario, y la fecha de log en formato yyyy_MM_DD_HH_mm_ss
# Autor: Luis Xavier

echo "Generating log file..."
touch log.txt

echo "Registering login..."
user=$USER
date=$(date +%Y_%m_%d__%H:%M:%S)

echo "$user/$date" >> log.txt

sleep 1
echo -e "Login Registered\n"
cat log.txt
```

## ****Empaquetamiento TAR, GZIP y PBZIP 2****

El empaquetamiento es un tema interesante para manejar respaldos u otro tipo de archivos para poder reducir el tamaño de uno o varios archivos para luego distribuirlos a través de la red u otra ubicación dentro del equipo.

- `tar`: permite empaqueta múltiples archivos
- `gzip`: Este solo nos permite empaquetar un único archivo, pero nos permite optimizar el tamaño del empaquetado. Suele usarse en conjunto con `tar`
- `pbzip2`: Este comando permite soporta el multicore, multiprocesador. Solo podemos empaquetar un solo archivo.

```bash
# ! /bin/bash
# Programa para ejemplificar el empaquetamiento con el comando tar
# Autor: Marco Toscano Freire - @martosfre

echo "Empaquetar todos los scripts de la carpeta shellCourse"
tar -cvf shellCourse.tar *.sh
```

```bash
# ! /bin/bash
# Programa para ejemplificar el empaquetamiento con el comando tar y gzip
# Autor: Marco Toscano Freire - @martosfre

echo "Empaquetar todos los scripts de la carpeta shellCourse"
tar -cvf shellCourse.tar *.sh

# Cuando se empaqueta con gzip el empaquetamiento anterior se elimina
gzip shellCourse.tar

echo "Empaquetar un solo archivo, con un ratio 9"
gzip -9 9_options.sh
```

```bash
# ! /bin/bash
# Programa para ejemplificar el empaquetamiento con el comando pbzip
# Autor: Marco Toscano Freire - @martosfre

echo "Empaquetar todos los scripts de la carpeta shellCourse"
tar -cvf shellCourse.tar *.sh
pbzip2 -f shellCourse.tar

echo "Empaquetar un directorio con tar y pbzip2"
tar -cf *.sh -c > shellCourseDos.tar.bz2

```

## ****Respaldo Empaquetado con clave****

![Untitled](Curso%20de%20P%20eaf6a/Untitled.png)

```bash
# ! /bin/bash
# Programa para ejemplificar el empaquetamiento con clave utilizando zip
# Autor: Marco Toscano Freire - @martosfre

echo "Empaquetar todos los scripts de la carpeta shellCourse con zip y asignarle una clave de seguridad"
zip -e shellCourse.zip *.sh
```

## ****Respaldo Empaquetado con clave****

![Untitled](Curso%20de%20P%20eaf6a/Untitled%201.png)

```bash
# ! /bin/bash
# Programa para ejemplificar el empaquetamiento con clave utilizando zip
# Autor: Marco Toscano Freire - @martosfre

echo "Empaquetar todos los scripts de la carpeta shellCourse con zip y asignarle una clave de seguridad"
zip -e shellCourse.zip *.sh
```

## ****Transferir información red****

```bash
# ! /bin/bash
# Programa para ejemplificar la forma de como transferir por la red utilizando el comando rsync, utilizando las opciones de empaquetamiento para optmizar la velocidad de transferencia
# Autor: Marco Toscano Freire - @martosfre

echo "Empaquetar todos los scripts de la carpeta shellCourse y transferirlos por la red a otro equpoutilizando el comando rsync"

host=""
usuario=""

read -p "Ingresar el host:" host
read -p "Ingresar el usuario:" usuario
echo -e "\nEn este momento se procederÃ¡ a empaquetar la carpeta y transferirla según los datos ingresados"
rsync -avz $(pwd) $usuario@$host:/Users/martosfre/Downloads/platzi
```

## Reto 6

```bash
# !/bin/bash
# Programa que muestra algunas funcionalidades basicas del sistema

option=0
usuario=$(logname)
fechaArchivo=$(date +"%F")
fechaAcceso=$(date +"%Y-%m-%d %H:%M:%S")
archivoPath=~/Backup
archivoName=log-$fechaArchivo.log

if [ -d $archivoPath ]; then
    if [ -f $archivoPath/$archivoName ]; then
        echo -e "\nAccedió el usuario: $usuario el día: $fechaAcceso" >> $archivoPath/$archivoName
    else
        touch $archivoPath/$archivoName
        echo -e "\nAccedió el usuario: $usuario el día: $fechaAcceso" >> $archivoPath/$archivoName
    echo -e "\n  Operaciones realizadas:\n" >> $archivoPath/$archivoName
    fi
else
    mkdir $archivoPath
    touch $archivoPath/$archivoName
    echo -e "\nAccedió el usuario: $usuario el día: $fechaAcceso" >> $archivoPath/$archivoName
    echo -e "\n  Operaciones realizadas:\n" >> $archivoPath/$archivoName
fi

#Impresion del menú
while :
do
    clear
    echo "------------------------------------------------"
    echo "-------------- Menú Principal ------------------"
    echo "------------------------------------------------"
    echo "-    1.- Procesos Actuales                     -"
    echo "-    2.- Memoria Disponible                    -"
    echo "-    3.- Espacio en Disco                      -"
    echo "-    4.- Información de Red                    -"
    echo "-    5.- Variables de entorno Configuradas     -"
    echo "-    6.- Información del Programa              -"
    echo "-    7.- Backup Información                    -"
    echo "-    8.- Salir                                 -"
    echo "------------------------------------------------"
    
    read -n1 -p "Ingrese la opción deseada [1-8]:  " option

    case $option in
    1) clear
        echo -e "\n\tProcesos Actuales\n"
        echo -e "\n\tProcesos Actuales\n" >> $archivoPath/$archivoName
        ps aux
        ps aux >> $archivoPath/$archivoName
        echo -e "\n"
        read -n1 -p "Presione una tecla para continuar..."
        ;;
    2) clear
        echo -e "\n\tMemoria Disponible\n" 
        echo -e "\n\tMemoria Disponible\n" >> $archivoPath/$archivoName
        free -h
        free -h >> $archivoPath/$archivoName
        echo -e "\n"
        read -n1 -p "Presione una tecla para continuar..."
        ;;
    3) clear
        echo -e "\n\tMemoria en disco\n" 
        echo -e "\n\tMemoria en disco\n" >> $archivoPath/$archivoName
        du -h
        du -h >> $archivoPath/$archivoName
        echo -e "\n"
        read -n1 -p "Presione una tecla para continuar..."
        ;;
    4) clear
        echo -e "\n\tInformación de Red\n" 
        echo -e "\n\tInformación de Red\n" >> $archivoPath/$archivoName
        ifconfig
        ifconfig >> $archivoPath/$archivoName
        echo -e "\n"
        read -n1 -p "Presione una tecla para continuar..."
        ;;
    5) clear
        echo -e "\n\tVariables de entorno configuradas\n"
        echo -e "\n\tVariables de entorno configuradas\n" >> $archivoPath/$archivoName
        printenv
        printenv >> $archivoPath/$archivoName
        echo -e "\n"
        read -n1 -p "Presione una tecla para continuar..."
        ;;
    6) clear
        echo -e "\n\tInformación del Sistema\n"
        echo -e "\n\tInformación del Sistema\n" >> $archivoPath/$archivoName
        echo -e "\tPrograma que realiza funcionalidades basicas del OS"
        echo -e "\tAutor: Adan Galicia"
        echo -e "\tInformacón de contacto: algo9854@gmail.com"
        echo -e "\n"
        read -n1 -p "Presione una tecla para continuar..."
        ;;
    7) clear
        echo -e "\n\tBackup Información\n"
        echo -e "\n\tRealizacion de Backup\n" >> $archivoPath/$archivoName
        read -p "Ingrese el host: " host
        read -p "Ingrese el usuario: " user
        read -p "Ingrese la ruta en donde quiera hacer el backup: " ruta
        
        zip -e backup-$fechaArchivo.zip $archivoPath/*.log
        rsync -avz backup-$fechaArchivo.zip $user@$host:$ruta
        ;;
    8) clear
        echo -e "\n\tAdios!\n"
        exit
        ;;
    *) clear
        echo -e "\n\tOpción no encontrada\n"
        read -n1 -p "Presione una tecla para continuar..."
        ;;
    esac
done
```

## ****Crear funciones y Paso de Argumentos****

![Untitled](Curso%20de%20P%20eaf6a/Untitled%202.png)

```bash
# ! /bin/bash
# Programa que permite manejar las utilidades de Postres
# Autor: Marco Toscano Freire - @martosfre

opcion=0

# Función para instalar postgres
instalar_postgres () {
    echo "Instalar postgres..."
}

# Función para desinstalar postgres
desinstalar_postgres () {
    echo "Desinstalar postres..."
}

# Función para sacar un respaldo
sacar_respaldo () {
    echo "Sacar respaldo..."
    echo "Directorio backup: $1"
}

# Función para restaurar un respaldo
restaurar_respaldo () {
    echo "Restaurar respaldo..."
    echo "Directorio respaldo: $1"
}

while :
do
    #Limpiar la pantalla
    clear
    #Desplegar el menú de opciones
    echo "_________________________________________"
    echo "PGUTIL - Programa de Utilidad de Postgres"
    echo "_________________________________________"
    echo "                MENÚ PRINCIPAL           "
    echo "_________________________________________"
    echo "1. Instalar Postgres"
    echo "2. Desinstalar Postgres"
    echo "3. Sacar un respaldo"
    echo "4. Restar respaldo"
    echo "5. Salir"

    #Leer los datos del usuario - capturar información
    read -n1 -p "Ingrese una opción [1-5]:" opcion

    #Validar la opción ingresada
    case $opcion in
        1)
            instalar_postgres
            sleep 3
            ;;
        2) 
            desinstalar_postgres
            sleep 3
            ;;
        3) 
            read -p "Directorio Backup:" directorioBackup
            sacar_respaldo $directorioBackup
            sleep 3
            ;;
        4) 
            read -p "Directorio de Respaldos:" directorioRespaldos
            restaurar_respaldo $directorioRespaldos
            sleep 3
            ;;
        5)  
            echo "Salir del Programa"
            exit 0
            ;;
    esac
done
```

## ****Funciones de instalar y desinstalar postgres****

```bash
# ! /bin/bash
# Programa que permite manejar las utilidades de Postres
# Autor: Marco Toscano Freire - @martosfre

opcion=0

# Función para instalar postgres
instalar_postgres () {
    echo -e "\n Verificar instalación postgres ...."
    verifyInstall=$(which psql)
    if [ $? -eq 0 ]; then
        echo -e "\n Postgres ya se encuentra instalado en el equipo"
    else
        read -s -p "Ingresar contraseña de sudo:" password
        read -s -p "Ingresar contraseña a utilizar en postgres:" passwordPostgres
        echo "$password" | sudo -S apt update
        echo "$password" | sudo -S apt-get -y install postgresql postgresql-contrib
        sudo -u postgres psql -c "ALTER USER postgres WITH PASSWORD '{$PASSWORDpOSTGRES}';"
        echo "$password" | sudo -S systemctl enable postgresql.service
        echo "$password" | sudo -S systemctl start postgresql.service
    fi    
    read -n 1 -s -r -p "PRESIONE [ENTER] para continuar..."
}

# Función para desinstalar postgres
desinstalar_postgres () {
    read -s -p "Ingresar contraseña de sudo:" password
    echo -e "\n"
    echo "$password" | sudo -S systemctl stop postgresql.service
    echo "$password" | sudo -S apt-get -y --purge remove postgresql\*
    echo "$password" | sudo -S rm -r /etc/postgresql
    echo "$password" | sudo -S rm -r /etc/postgresql-common
    echo "$password" | sudo -S rm -r /var/lib/postgresql
    echo "$password" | sudo -S userdel -r postgres
    echo "$password" | sudo -S groupdel postgresql
    read -n 1 -s -r -p "PRESIONE [ENTER] para continuar..."
}

# Función para sacar un respaldo
sacar_respaldo () {
    echo "Sacar respaldo..."i
    echo "Directorio backup: $1"
}

# Función para restaurar un respaldo
restaurar_respaldo () {
    echo "Restaurar respaldo..."
    echo "Directorio respaldo: $1"
}

while :
do
    #Limpiar la pantalla
    clear
    #Desplegar el menú de opciones
    echo "_________________________________________"
    echo "PGUTIL - Programa de Utilidad de Postgres"
    echo "_________________________________________"
    echo "                MENÚ PRINCIPAL           "
    echo "_________________________________________"
    echo "1. Instalar Postgres"
    echo "2. Desinstalar Postgres"
    echo "3. Sacar un respaldo"
    echo "4. Restar respaldo"
    echo "5. Salir"

    #Leer los datos del usuario - capturar información
    read -n1 -p "Ingrese una opción [1-5]:" opcion

    #Validar la opción ingresada
    case $opcion in
        1)
            instalar_postgres
            sleep 3
            ;;
        2) 
            desinstalar_postgres
            sleep 3
            ;;
        3) 
            read -p "Directorio Backup:" directorioBackup
            sacar_respaldo $directorioBackup
            sleep 3
            ;;
        4) 
            read -p "Directorio de Respaldos:" directorioRespaldos
            restaurar_respaldo $directorioRespaldos
            sleep 3
            ;;
        5)  
            echo "Salir del Programa"
            exit 0
            ;;
    esac
done
```

## ****Funciones sacar y restaurar respaldos en postgres****

```bash
# ! /bin/bash
# Programa que permite manejar las utilidades de Postres
# Autor: Marco Toscano Freire - @martosfre

opcion=0
fechaActual=`date +%Y%m%d`

# Función para instalar postgres
instalar_postgres () {
    echo -e "\n Verificar instalación postgres ...."
    verifyInstall=$(which psql)
    if [ $? -eq 0 ]; then
        echo -e "\n Postgres ya se encuentra instalado en el equipo"
    else
        echo -e "\n"
        read -s -p "Ingresar contraseña de sudo:" password
        read -s -p "Ingresar contraseña a utilizar en postgres:" passwordPostgres
        echo "$password" | sudo -S apt update
        echo "$password" | sudo -S apt-get -y install postgresql postgresql-contrib
        sudo -u postgres psql -c "ALTER USER postgres WITH PASSWORD '{$PASSWORDpOSTGRES}';"
        echo "$password" | sudo -S systemctl enable postgresql.service
        echo "$password" | sudo -S systemctl start postgresql.service
    fi
    read -n 1 -s -r -p "PRESIONE [ENTER] para continuar..."
}

# Función para desinstalar postgres
desinstalar_postgres () {
    echo -e "\n"
    read -s -p "Ingresar contraseña de sudo:" password
    echo -e "\n"
    echo "$password" | sudo -S systemctl stop postgresql.service
    echo "$password" | sudo -S apt-get -y --purge remove postgresql\*
    echo "$password" | sudo -S rm -r /etc/postgresql
    echo "$password" | sudo -S rm -r /etc/postgresql-common
    echo "$password" | sudo -S rm -r /var/lib/postgresql
    echo "$password" | sudo -S userdel -r postgres
    echo "$password" | sudo -S groupdel postgresql
    read -n 1 -s -r -p "PRESIONE [ENTER] para continuar..."
}

# Función para sacar un respaldo
sacar_respaldo () {
    echo "Listar las bases de datos"
    sudo -u postgres psql -c "\l"
    read -p "Elegir la base de datos a respaldar:" bddRespaldo
    echo -e "\n"
    if [ -d "$1" ]; then
        echo "Establecer permisos directorio"
        echo "$password" | sudo -S chmod 755 $1
        echo "Realizando respaldo..."
        sudo -u postgres pg_dump -Fc $bddRespaldo > "$1/bddRespaldo$fechaActual.bak"
        echo "Respaldo realizado correctamente en la ubicación:$1/bddRespaldo$fechaActual.bak"
    else
        echo "El directorio $1 no existe"
    fi
    read -n 1 -s -r -p "PRESIONE [ENTER] para continuar..."
}

# Función para restaurar un respaldo
restaurar_respaldo () {
    echo "Listar respaldos"
    ls -1 $1/*.bak
    read -p "Elegir el respaldo a restaurar:" respaldoRestaurar
    echo -e "\n"
    read -p "Ingrese el nombre de la base de datos destino:" bddDestino
    #Verificar si la bdd existe
    verifyBdd=$(sudo -u postgres psql -lqt | cut -d \| -f 1 | grep -wq $bddDestino)
    if [ $? -eq 0 ]; then
        echo "Restaurando en la bdd destino: $bddDestino"
    else
        sudo -u postgres psql -c "create database $bddDestino"
    fi

    if [ -f "$1/$respaldoRestaurar" ]; then
        echo "Restaurando respaldo..."
        sudo -u postgres pg_restore -Fc -d $bddDestino "$1/$respaldoRestaurar"
        echo "Listar la base de datos"
        sudo -u postgres psql -c "\l"
    else
        echo "El respaldo $respaldoRestaurar no existe"
    fi
    read -n 1 -s -r -p "PRESIONE [ENTER] para continuar..."
}

while :
do
    #Limpiar la pantalla
    clear
    #Desplegar el menú de opciones
    echo "_________________________________________"
    echo "PGUTIL - Programa de Utilidad de Postgres"
    echo "_________________________________________"
    echo "                MENÚ PRINCIPAL           "
    echo "_________________________________________"
    echo "1. Instalar Postgres"
    echo "2. Desinstalar Postgres"
    echo "3. Sacar un respaldo"
    echo "4. Restar respaldo"
    echo "5. Salir"

    #Leer los datos del usuario - capturar información
    read -n1 -p "Ingrese una opción [1-5]:" opcion

    #Validar la opción ingresada
    case $opcion in
        1)
            instalar_postgres
            sleep 3
            ;;
        2)
            desinstalar_postgres
            sleep 3
            ;;
        3)
            echo -e "\n"
            read -p "Directorio Backup:" directorioBackup
            sacar_respaldo $directorioBackup
            sleep 3
            ;;
        4)
            echo -e "\n"
            read -p "Directorio de Respaldos:" directorioRespaldos
            restaurar_respaldo $directorioRespaldos
            sleep 3
            ;;
        5)
            echo "Salir del Programa"
            exit 0
            ;;
    esac
done
```

## Reto 7

```bash
# ! /bin/bash
 # Programa para cumplir con el reto#3
 #Arnoldo Alvarez
 
 opcion=""
 numA=0
 numB=0
 numC=0
 #telRegex= '^\(?([0-9]{3})\)?([0-9]{3})[.]?([0-9]{4})$' #Solo acepta el formato telefonico (xxx)xxx.xxxx Ej:(706)612.4602
 telRegex2='^\([0-9]\{3\}\)\([0-9]\{3\}\)\([0-9]*\)/(\1) \2 . \3/$'
 pathArchivo=""
 aritmetica=""
 funcion=""
 phone=""
 respTel=""
 respBackup=""
 FILE=log.txt
 FILE2=Zip.zip
 DATE=`date +%y%m%d`
 TIME=`date +%H%M%S`
 
 coronavirus_guidelines() {
 
          echo -e "\nLo que debes hacer es lo siguiente:
               a) Lavarse las manos frecuentemente.
               b) Toser o estornudar al interior de  tu codo.
               c) No tocarse la cara.
               d) Mantener cierta distancia social.
               e) Quedarse voluntariamente en casa."
 
               echo "$DATE-$TIME --- Guidelines de CoronaVirus consultadas" >> logs_reto7/$NEWFILE
 
      read -n 1 -s -r -p "Presione [ENTER] para continuar..."
  }
Math_Function () {
 
  echo    "Funciones Aritmeticas disponibles
                      1.- Sumar
                      2.- Multiplicar
                      3.- Dividir"
           echo -e "\n"
           read -p "Escoja la funcion Aritmetica: " aritmetica
 
           case $aritmetica in
 
                "1")  funcion="suma"
                      numC=$((numA + numB));;
                "2")  funcion="Multiplicacion"
                     numC=$((numA * numB));;
                "3")  funcion="Division"
                      numC=$((numA / numB));;
                  *)  funcion="Funcion No definida"
                      echo "$DATE-$TIME --- Opcion No encontrada,Funcion Matematica NO realizada"   >> logs_reto6/$NEWFILE
                      echo "Opcion incorrecta";;
           esac
 
              echo "Resultado Matematico de la $funcion: $numC "
              echo "$DATE-$TIME --- Usuario realiza funcion matematica $funcion:$numC" >> logs_reto7/$NEWFILE
 
      read -n 1 -s -r -p "Presione [ENTER] para continuar..."
 
 }
Phone_Format () {
 
      echo "$DATE-$TIME --- Usuario escoge chequear formato de numero telefonico" >> logs_reto7/$NEWFILE
              read -p "Ingrese numero telefonico: " telefono
 
              if [[ $telefono =~ $telRegex2 ]]; then
                  echo "Formato correcto dentro de los EEUU"
              else
              phone=$telefono
              plainPhone=$(echo $phone | sed "s/[()-.]//g")
              echo "Formato Incorrecto dentro de los EEUU"
              read -n1 -p "Convertir al formato (123)456.7890 s/n:  "  respTel
              echo  -e "\n"
               if [ $respTel = "s" ]; then
                formatedPhone2=$(echo $plainPhone | sed "s/\([0-9]\{3\}\)\([0-9]\{3\}\)\([0-9]*\)/(\1) \2 . \3/")
                echo "Numero convertido: $formatedPhone2 "
                echo "$DATE-$TIME --- Usuario cambia formato del Numero Telefonico $telefono" >> logs_reto7/$NEWFILE
               else
 
                   echo "$DATE-$TIME --- Usuario responde NO para cambiar formato de  $telefono" >> logs_reto7/$NEWFILE
                   echo "Volviendo al Menu Principal..."
               fi
              fi
 
      read -n 1 -s -r -p "Presione [ENTER] para continuar..."
 }
Directory_Search () {
 
      if [[ -d $dirPath  ]]; then
 
                  echo "$DATE-$TIME --- Usuario consulta satisfactoriamente el directorio $dirPath" >> logs_reto7/$NEWFILE
                  echo "El directorio $dirPath SI Existe"
 
                  else
                      echo "El directorio NO Existe o NO es un directorio"
                      echo "$DATE-$TIME --- Usuario No encuentra $dirPath" >> logs_reto7/$NEWFILE
              fi
 
      read -n 1 -s -r -p "Presione [ENTER] para continuar..."
 }
 
 File_Search () {
 
     if [[ -e $filePath  ]]; then
               echo "$DATE-$TIME --- Usuario consulta el archivo $filePath" >> logs_reto7/$NEWFILE
               cat $filePath
           else
               echo "No se encuentra el archivo o Nombre de archivo Incorrecto"
               echo "$DATE-$TIME --- Usuario No encuentra $filePath" >> logs_reto7/$NEWFILE
           fi
 
      read -n 1 -s -r -p "Presione [ENTER] para continuar..."
 
 }
Backup_Shit () {
 
     if [[ $respBackup = "s" ]]; then
               echo -e  "\ncreando archivo tar..."
               sleep 2
               tar -cvf logs_reto7/backup_`date +%Y%m%d`_`date +%H%M%S`.tar logs_reto7/
 
               echo -e "\nCreando archivo ZIP..."
               echo "Debera introducir una Clave de Seguridad..."
               sleep 2
               zip -e logs_reto7/zip_`date +%Y%m%d`_`date +%H%M%S`.zip /shellCourse/logs_reto7/*.tar
 
               echo "Transfieriendo archivo ZIP..."
               echo "Clave de Administrador para Transferencias"
               sleep 2
               rsync -avz /shellCourse/logs_reto7/*.zip a2419@192.168.1.9:/$HOME/backup_logs_reto7/
               echo "$DATE-$TIME --- Usuario ejecutando proceso de Respaldo" >> logs_reto7/$NEWFILE
               sleep 3
               echo -e  "\nBackup Realizado con Exito..."
           else
 
               echo "$DATE-$TIME --- Usuario cancela proceso de Respaldo " >> logs_reto7/$NEWFILE
               echo -e "\nSaliendo del modulo de Respaldos..."
               sleep 3
           fi
  }
 #Se crea un archivo .log con fecha y hora y se mueve a un directorio de logs_reto5
 NEWFILE=${FILE%.*}_`date +%Y%m%d`_`date +%H%M%S`.${FILE#*.}
 touch $NEWFILE
 mv $NEWFILE logs_reto6/
  #echo "El archivo $NEWFILE fue creado con exito"
 
 
 while :
 do
     clear
     echo "archivo: $NEWFILE"
 echo "Las opciones son las siguientes\n
         1.- Para Saber como evitar CoronaVirus
         2.- Realizar funciones numericas
         3.- Para verificar formato de numero telefonico
         4.- Para verificar un directorio
         5.- Ver contenido de un Archivo
         6.- Hacer Respaldo de Logs
         7.- salir"
 
 echo -e "\n"
 read -n1  -p "Introduzca su Opcion: " opcion
case $opcion in
 
     "1") coronavirus_guidelines
 
          ;;
 
     "2") echo -e "\nIntroduzca el numero A: "
          read
          numA=$REPLY
          echo -e "Introduzca el numero B: "
          read
          numB=$REPLY
          Math_Function $numA $numB
 
          ;;
 
 
      "3")   echo -e "\n"
             Phone_Format
             ;;
"4") echo -e "\n"
          read -p "Ingrese la ruta de un directorio: " dirPath
          Directory_Search $dirPath
         ;;
 
      "5")echo -e "\n"
          read -p "Ingrese la ruta del archivo: " filePath
          File_Search $filePath
          ;;
 
      "6")echo -e "\n"
          read -n1 -p "Desea hacer Backup del Directorio logs_reto7 s/n: " respBackup
          Backup_Shit $respBackup
 
          ;;
 
      "7")   echo -e "\n"
             echo -e "Saliendo..."
             echo "$DATE-$TIME --- Usuario sale de la aplicacion" >> logs_reto7/$NEWFILE
             exit 0
 
             ;;
 
       *) echo "Opcion Incorrecta, Lo sentimos"
 
 
       esac
 done
```

## Cheatsheet

[https://devhints.io/bash](https://devhints.io/bash)
