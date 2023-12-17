# blockchain

import hashlib
import time

class Bloque:
    def __init__(self, indice, marca_tiempo, datos, hash_anterior):
        self.indice = indice
        self.marca_tiempo = marca_tiempo
        self.datos = datos
        self.hash_anterior = hash_anterior
        self.hash = self.calcular_hash()

    def calcular_hash(self):
        datos_concatenados = str(self.indice) + str(self.marca_tiempo) + str(self.datos) + str(self.hash_anterior)
        return hashlib.sha256(datos_concatenados.encode('utf-8')).hexdigest()

def crear_bloque(datos, cadena_anterior=None):
    indice = (cadena_anterior.indice + 1) if cadena_anterior else 0
    marca_tiempo = time.time()
    hash_anterior = cadena_anterior.hash if cadena_anterior else 0
    return Bloque(indice, marca_tiempo, datos, hash_anterior)

# Crear el bloque génesis (primer bloque)
bloque_genesis = Bloque(0, time.time(), "Datos del bloque génesis", 0)
cadena_de_bloques = [bloque_genesis]

# Agregar algunos bloques a la cadena
bloque1 = crear_bloque("Datos del bloque 1", cadena_de_bloques[-1])
cadena_de_bloques.append(bloque1)

bloque2 = crear_bloque("Datos del bloque 2", cadena_de_bloques[-1])
cadena_de_bloques.append(bloque2)

# Mostrar la cadena de bloques
for bloque in cadena_de_bloques:
    print(f"Índice: {bloque.indice}")
    print(f"Marca de tiempo: {bloque.marca_tiempo}")
    print(f"Datos: {bloque.datos}")
    print(f"Hash anterior: {bloque.hash_anterior}")
    print(f"Hash: {bloque.hash}")
    print("\n")
