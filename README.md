# masia
masia
def imprimir_tablero(tablero):
    print("\n")
    for fila in tablero:
        print(" | ".join(fila))
        print("-" * 9)


def verificar_ganador(tablero, jugador):
    # Revisar filas, columnas y diagonales
    for i in range(3):
        if all([celda == jugador for celda in tablero[i]]):  # filas
            return True
        if all([tablero[j][i] == jugador for j in range(3)]):  # columnas
            return True
    # diagonales
    if all([tablero[i][i] == jugador for i in range(3)]):
        return True
    if all([tablero[i][2 - i] == jugador for i in range(3)]):
        return True
    return False


def tablero_lleno(tablero):
    return all([celda != " " for fila in tablero for celda in fila])


def jugar():
    tablero = [[" " for _ in range(3)] for _ in range(3)]
    jugador_actual = "X"

    while True:
        imprimir_tablero(tablero)
        print(f"Turno de {jugador_actual}")
        try:
            fila = int(input("Elige fila (0, 1, 2): "))
            columna = int(input("Elige columna (0, 1, 2): "))
        except ValueError:
            print("Por favor, introduce un número válido.")
            continue

        if 0 <= fila <= 2 and 0 <= columna <= 2:
            if tablero[fila][columna] == " ":
                tablero[fila][columna] = jugador_actual
                if verificar_ganador(tablero, jugador_actual):
                    imprimir_tablero(tablero)
                    print(f"¡Jugador {jugador_actual} gana!")
                    break
                elif tablero_lleno(tablero):
                    imprimir_tablero(tablero)
                    print("¡Empate!")
                    break
                jugador_actual = "O" if jugador_actual == "X" else "X"
            else:
                print("Esa casilla ya está ocupada. Elige otra.")
        else:
            print("Fila o columna fuera de rango. Usa 0, 1 o 2.")

if __name__ == "__main__":
    jugar()
