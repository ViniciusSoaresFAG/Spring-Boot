﻿# Spring-Boot .
# teste
# testeimport java.util.Scanner;

public class JogoDaVelha {

    public static void main(String[] args) {
        char[][] tabuleiro = {
            {' ', ' ', ' '},
            {' ', ' ', ' '},
            {' ', ' ', ' '}
        };

        boolean jogoEmAndamento = true;
        char jogadorAtual = 'X';

        while (jogoEmAndamento) {
            exibirTabuleiro(tabuleiro);
            fazerJogada(tabuleiro, jogadorAtual);

            if (verificarVitoria(tabuleiro, jogadorAtual)) {
                exibirTabuleiro(tabuleiro);
                System.out.println("Jogador " + jogadorAtual + " venceu!");
                jogoEmAndamento = false;
            } else if (tabuleiroCheio(tabuleiro)) {
                exibirTabuleiro(tabuleiro);
                System.out.println("O jogo empatou!");
                jogoEmAndamento = false;
            } else {
                jogadorAtual = (jogadorAtual == 'X') ? 'O' : 'X';
            }
        }
    }

    public static void exibirTabuleiro(char[][] tabuleiro) {
        System.out.println("  0 1 2");
        for (int i = 0; i < 3; i++) {
            System.out.print(i + " ");
            for (int j = 0; j < 3; j++) {
                System.out.print(tabuleiro[i][j]);
                if (j < 2) {
                    System.out.print("|");
                }
            }
            System.out.println();
            if (i < 2) {
                System.out.println("  -----");
            }
        }
        System.out.println();
    }

    public static void fazerJogada(char[][] tabuleiro, char jogador) {
        Scanner scanner = new Scanner(System.in);
        int linha, coluna;

        do {
            System.out.print("Jogador " + jogador + ", informe a linha (0, 1 ou 2): ");
            linha = scanner.nextInt();
            System.out.print("Jogador " + jogador + ", informe a coluna (0, 1 ou 2): ");
            coluna = scanner.nextInt();
        } while (!jogadaValida(tabuleiro, linha, coluna));

        tabuleiro[linha][coluna] = jogador;
    }

    public static boolean jogadaValida(char[][] tabuleiro, int linha, int coluna) {
        return linha >= 0 && linha < 3 && coluna >= 0 && coluna < 3 && tabuleiro[linha][coluna] == ' ';
    }

    public static boolean verificarVitoria(char[][] tabuleiro, char jogador) {
        for (int i = 0; i < 3; i++) {
            if ((tabuleiro[i][0] == jogador && tabuleiro[i][1] == jogador && tabuleiro[i][2] == jogador) ||
                (tabuleiro[0][i] == jogador && tabuleiro[1][i] == jogador && tabuleiro[2][i] == jogador)) {
                return true;
            }
        }

        return (tabuleiro[0][0] == jogador && tabuleiro[1][1] == jogador && tabuleiro[2][2] == jogador) ||
               (tabuleiro[0][2] == jogador && tabuleiro[1][1] == jogador && tabuleiro[2][0] == jogador);
    }

    public static boolean tabuleiroCheio(char[][] tabuleiro) {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (tabuleiro[i][j] == ' ') {
                    return false;
                }
            }
        }
        return true;
    }
}
