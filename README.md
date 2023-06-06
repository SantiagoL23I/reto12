# reto12
## endswith 
# devuelve true si la cadena termina con el valor que se le especifique, si no lo hace develve false
## starswith 
# devuelve true si la cadena empieza con el valor que se le especifique, si no lo hace develve false
## isalpha 
# devuelve true si loscaracteres sin letras
## isalnum
# devuelve true si son caracteres alfanumericos
## isdigit
# devuelve true si lo caracteres son digitos
 ## isspace
# devuelve true si lo caracteres son espacios en blanco
## istitle 
# devuelve true solo si las paabras en un texto empiezan en mayuscula
## islower
# devuelve true si todos los caracteres son minusculas
## ISUPPER 
# DEVUELVE TRUE SI TODOS LOS CARACTERES ESTAN EN MAYUSCULA
2. #vocales
``psudocode 
file = open ( 'Archivo.text') # Importael archivo de texto
texto= (file.read()) # El archivo de texto se depositan una variable
texto=texto.lower() # Vuelvetodo el texto en minusculas
lista=["b", "c", "d", "f", "g", "h", "j", "k", "l", "m", "n", "ñ", "p", "q", "r", "s", "t", "v", "x", "z", "w", "y"] # Lista de consonantes
consontante= 0 # Variable consonante que sera igual a 0 
for j in range (0,len(lista)): # For donde se recorre cada letra que hay en la lista
   consontante += (texto.count(lista[j])) # La consonante = la cantidad de palabras que hay en el texto y que hay en la lista
print("La cantidad de consonantes son:" +str(vocales))
3. #consonantes
4. ``pseudocode
file= open ( 'Archivo.text') # Importael archivo de texto
texto= (file.read()) # El archivo de texto seepositaen una variable
texto=texto.lower() # Vuelvetodo el texto en minusculas
lista=["a","e","i","o","u"] # Lista de las vocales
vocales= 0 # Variable vocales que sera igual a 0
for j in range (0,len(lista)): # Recorrela lista desde el incio hasta el final
   vocales += (texto.count(lista[j])) # Las vocales = la cantidad de palabras que hay en el texto y que hay en la lista
print("La cantidad de consonantes es" +str(consonante))
 ``
#3 palabras que se repiten
``pseudocode
file = open('texto.txt', "r")  dicpalabras = {} 
# Se crea un diccionario en donde se guardaran todas las palabras del texto  for line in file: 
# Por cada linea en el archivo 
    linea = line.split() # Se crea un lista por cada linea, en donde saldran todas las palabras separadas por espacios      for palabra in linea: 
# Por cada palabra de la lista          if palabra in dicpalabras: 
# Si la palabra esta en el diccionario, el valor de la llave aumenta en uno               dicpalabras[palabra] += 1 
         else:              dicpalabras[palabra] = 1
 # Si no esta en el diccionario, la palabra se agrega en el diccionario con el valor de uno  listadepalabras = list(dicpalabras.items()) 
# Se convierte el diccionario en un lista de tuplas  print("lista de palabras con la cantidad de veces que aparece: ", listadepalabras)  listadepalabras.sort(key=lambda x: x[1], reverse=True) 
# Funcion lamba para ordenar de mayor a menor, ordena segun el segundo elemento del diccionario  c50palabras = listadepalabras[:50] 
# Improme hasta el valor anterior al 50 
 print("Palabras que mas aparecen:") 
 for palabra, veces in c50palabras:
# se imprime las 50 palabras y la cantidad de veces     print(palabra,":",veces)
  ``
#4 listado de destinatario recibido
```pseudocode
def obtener_destinatarios(archivo):
    destinatarios = {}
    with open(archivo, 'r') as f:
        for linea in f:
            if linea.startswith('Received:'):
                correo = obtenerCorreo(linea)
                if correo:
                    destinatarios[correo] = destinatarios.get(correo, 0) + 1

    return destinatarios
def obtenerCorreo(linea):
    inicio = linea.find('from ') + 5
    fin = linea.find(' ', inicio)
    correo = linea[inicio:fin]
    return correo
archivo = 'mbox-short (1).txt'
resultados = obtener_destinatarios(archivo)
for correo, cantidad in resultados.items():
    print(f'{correo}: {cantidad}')
  ```
#5 listado mensajes enviados 
``psudocode
def mensajesdiarios(texto: str) -> dict:
    recibidos = []  # Lista de segmentos del texto que contienen la información de la fecha.
    palabras = texto.split()  # Lista de cadenas de cada palabra en el texto.
    segmento = []  # Lista temporal para almacenar cada segmento encontrado
    
    for palabra in palabras:  # Bucle for para iterar sobre las palabras en el texto
        if palabra == "Received:":  # Verificar si la palabra actual es "Received:"
            segmento = [palabra]  # Crear un nuevo segmento con la palabra actual
        elif "-0500" in palabra or "(GMT)" in palabra:  # Verificar si se encontró el final de un segmento
            if segmento:  # Verificar si hay palabras en el segmento actual antes de agregarlo
                recibidos.append(segmento)
            segmento = []  # Reiniciar el segmento para el próximo conjunto de palabras
        elif segmento:  # Verificar si hay un segmento actual en el que agregar la palabra
            segmento.append(palabra)
    
    mensajes_por_dia = {}  # Se crea un diccionario para almacenar el día y el número de mensajes enviados.
    for segmento in recibidos:
        indice = segmento.index('Jan')  # Índice de la palabra "Jan".
        dia = int(segmento[indice - 1])  # Se extrae el día en función del índice de "Jan".
        if dia in mensajes_por_dia:  # Bloque de código para llenar el diccionario.
            mensajes_por_dia[dia] += 1
        else:
            mensajes_por_dia[dia] = 1

    return mensajes_por_dia

if _name_ == "_main_":
    file = open('texto.txt', "r")
    for line in file:
        numeros_dia = mensajesdiarios(file.read())
        for dia in numeros_dia:
            print("Se enviaron", numeros_dia[dia] , " mensajes el" ,dia,  "de enero del 2008")
