# Chat_Game_Para_Todos
Chat_Game_Para_Todos - DIO


#include <iostream>

// Função para imprimir a grade do jogo
void imprimirGrade(char grade[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            std::cout << grade[i][j] << " ";
        }
        std::cout << std::endl;
    }
}

// Função para verificar se há um vencedor
bool verificarVencedor(char grade[3][3], char jogador) {
    // Verificar linhas e colunas
    for (int i = 0; i < 3; i++) {
        if (grade[i][0] == jogador && grade[i][1] == jogador && grade[i][2] == jogador)
            return true;

        if (grade[0][i] == jogador && grade[1][i] == jogador && grade[2][i] == jogador)
            return true;
    }

    // Verificar diagonais
    if (grade[0][0] == jogador && grade[1][1] == jogador && grade[2][2] == jogador)
        return true;

    if (grade[0][2] == jogador && grade[1][1] == jogador && grade[2][0] == jogador)
        return true;

    return false;
}

int main() {
    char grade[3][3] = { { ' ', ' ', ' ' }, { ' ', ' ', ' ' }, { ' ', ' ', ' ' } };
    char jogadorAtual = 'X';
    int linha, coluna;

    // Loop principal do jogo
    while (true) {
        // Imprimir a grade atual
        imprimirGrade(grade);

        // Obter a jogada do jogador atual
        std::cout << "Jogador " << jogadorAtual << ", digite a linha e coluna da sua jogada: ";
        std::cin >> linha >> coluna;

        // Verificar se a jogada é válida
        if (linha < 0 || linha >= 3 || coluna < 0 || coluna >= 3 || grade[linha][coluna] != ' ') {
            std::cout << "Jogada inválida. Tente novamente!" << std::endl;
            continue;
        }

        // Fazer a jogada
        grade[linha][coluna] = jogadorAtual;

        // Verificar se há um vencedor
        if (verificarVencedor(grade, jogadorAtual)) {
            std::cout << "Parabéns! Jogador " << jogadorAtual << " venceu o jogo!" << std::endl;
            break;
        }

        // Verificar se o jogo terminou em empate
        bool jogoEmpatado = true;
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (grade[i][j] == ' ') {
                    jogoEmpatado = false;
                    break;
                }
            }
            if (!jogoEmpatado)
                break;
        }

        if (jogoEmpatado) {
            std::cout << "O jogo terminou em empate!" << std::endl;
            break;
        }

        // Alternar para o próximo jogador
        jogadorAtual = (jogadorAtual == 'X') ? 'O' : 'X';
    }

    return 0;
}
