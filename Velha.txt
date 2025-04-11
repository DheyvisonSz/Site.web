# Função para imprimir o tabuleiro
def print_board(board):
    for row in board:
        print(" | ".join(row))
        print("-" * 5)

# Função para verificar se alguém ganhou
def check_win(board, player):
    # Verificando linhas, colunas e diagonais
    for i in range(3):
        if all([cell == player for cell in board[i]]) or all([board[j][i] == player for j in range(3)]):
            return True
    if board[0][0] == player and board[1][1] == player and board[2][2] == player:
        return True
    if board[0][2] == player and board[1][1] == player and board[2][0] == player:
        return True
    return False

# Função para verificar empate
def check_tie(board):
    return all(cell != " " for row in board for cell in row)

# Função principal do jogo
def tic_tac_toe():
    # Solicita o nome dos jogadores
    player1 = input("Digite o nome do jogador 1 (X): ")
    player2 = input("Digite o nome do jogador 2 (O): ")

    board = [[" " for _ in range(3)] for _ in range(3)]
    current_player = "X"
    current_name = player1

    while True:
        print_board(board)
        print(f"Jogador {current_name} ({current_player}), faça sua jogada (linha, coluna):")
        try:
            row, col = map(int, input("Digite as coordenadas (linha, coluna) entre 0 e 2: ").split(","))
            if board[row][col] != " ":
                print("Esse espaço já está ocupado. Tente novamente.")
                continue
            board[row][col] = current_player
        except (ValueError, IndexError):
            print("Coordenadas inválidas. Tente novamente.")
            continue
        
        if check_win(board, current_player):
            print_board(board)
            print(f"Jogador {current_name} venceu!")
            break
        if check_tie(board):
            print_board(board)
            print("Empate!")
            break
        
        if current_player == "X":
            current_player = "O"
            current_name = player2
        else:
            current_player = "X"
            current_name = player1

    # Créditos
    print("\nJogo desenvolvido por Ryan Pietro. Obrigado por jogar!")

# Iniciar o jogo
tic_tac_toe()
