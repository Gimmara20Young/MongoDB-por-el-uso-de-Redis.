# MongoDB-por-el-uso-de-Redis.
En base a la aplicación desarrollada(Diccionario) en la Sustitución de SQL por MongoDB, debe sustituir el uso de MongoDB por el uso de Redis

import redis
client = redis.Redis(host = '127.0.0.1', port = 6379, db=0)

def agregar_palabra(palabra, significado):
	client.set(palabra,significado)

def editar_palabra(palabra):
    x=client.exists(palabra)
    if x==1:
        nuevo_significado= input("Ingrese el nuevo significado: ")
        client.set(palabra,nuevo_significado)
    else:
        print("Esta palabra no existe")

def buscar_significado_palabra(palabra):
	print(client.get(palabra))

def obtener_palabras():
    print(client.keys('*'))

def eliminar_palabra(palabra):
    client.delete(palabra)

def principal():

    menu = """
1) Agregar nueva palabra
2) Editar palabra existente
3) Buscar significado de palabra
4) Ver listado de palabras
5) Eliminar palabra existente
6) Salir
Elige: """
    eleccion = ""
    while eleccion != "6":
        eleccion = input(menu)
        if eleccion == "1":
            palabra = input("Ingresa la palabra: ")
            significado = input("Ingresa el significado: ")
            agregar_palabra(palabra,significado)
            print("Palabra agregada")

        if eleccion == "2":
            palabra = input("Ingresa la palabra que quiere editar: ")
            editar_palabra(palabra)

        if eleccion == "3":
            palabra = input("Ingresa la palabra del significado que quieres ver: ")
            buscar_significado_palabra(palabra)

        if eleccion == "4":
            obtener_palabras()

        if eleccion == "5":
            palabra = input("Ingrese la palabra a eliminar: ")
            eliminar_palabra(palabra)
            print("Palabra eliminada")


if __name__ == '__main__':
    principal()
