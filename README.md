# Sistema-bancario-
Projeto de sistemas bancario
#include <stdio.h>
#include <string.h>

#define MAX_CONTAS 2

typedef struct {
    char usuario[20];
    char senha[20];
    float saldo;
} Conta;

int login(Conta contas[], int qtd) {
    char usuario[20];
    char senha[20];

    printf("Digite seu usuario: ");
    scanf("%s", usuario);
    printf("Digite sua senha: ");
    scanf("%s", senha);

    for(int i = 0; i < qtd; i++) {
        if(strcmp(contas[i].usuario, usuario) == 0 && strcmp(contas[i].senha, senha) == 0) {
            return i; // retorna índice da conta
        }
    }
    return -1; // login inválido
}

int main() {
    Conta contas[MAX_CONTAS] = {
        {"alice", "1234", 1500.0},
        {"bob", "4321", 2000.0}
    };
    
    int indiceConta;
    int opcao;
    float valor;

    printf("=== Bem-vindo ao Banco Simulado ===\n");

    // Login
    while(1) {
        indiceConta = login(contas, MAX_CONTAS);
        if(indiceConta != -1) {
            printf("Login realizado com sucesso!\n");
            break;
        } else {
            printf("Usuario ou senha incorretos. Tente novamente.\n");
        }
    }

    // Menu principal
    while(1) {
        printf("\nEscolha uma opcao:\n");
        printf("1 - Consultar saldo\n");
        printf("2 - Depositar\n");
        printf("3 - Sacar\n");
        printf("4 - Sair\n");
        printf("Opcao: ");
        scanf("%d", &opcao);

        if(opcao == 1) {
            printf("Seu saldo atual e: R$ %.2f\n", contas[indiceConta].saldo);
        }
        else if(opcao == 2) {
            printf("Digite o valor a depositar: R$ ");
            scanf("%f", &valor);
            if(valor > 0) {
                contas[indiceConta].saldo += valor;
                printf("Deposito realizado com sucesso!\n");
            } else {
                printf("Valor invalido!\n");
            }
        }
        else if(opcao == 3) {
            printf("Digite o valor a sacar: R$ ");
            scanf("%f", &valor);
            if(valor > 0 && valor <= contas[indiceConta].saldo) {
                contas[indiceConta].saldo -= valor;
                printf("Saque realizado com sucesso!\n");
            } else {
                printf("Saldo insuficiente ou valor invalido!\n");
            }
        }
        else if(opcao == 4) {
            printf("Saindo do sistema. Obrigado!\n");
            break;
        }
        else {
            printf("Opcao invalida! Tente novamente.\n");
        }
    }

    return 0;
}