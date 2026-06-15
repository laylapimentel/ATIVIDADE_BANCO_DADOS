// Bacharelado interdisciplinar em Ciência e Tecnologia
// Disciplina: Laboratorio de Programação - 2N12
// Discente: Layla Pimenetel de Sousa
// Matricula: 20240005439

#include <stdio.h>
#include <string.h>

#define MAX_REGISTROS 50
#define MAX_LETRAS 30

char banco_dados[MAX_REGISTROS][MAX_LETRAS];

int buscarNome(char nome[]) {
    int i;
    for (i = 0; i < MAX_REGISTROS; i++) {
        if (strcmp(banco_dados[i], nome) == 0) {
            return i;
        }
    }
    return -1;
}

void addNome() {
    char nome[MAX_LETRAS];
    int i;
    printf("Digite o nome que deseja adicionar: ");
    scanf(" %29[^\n]", nome);

    if (buscarNome(nome) != -1) {
        printf("Erro! Nome ja existe. Digite um nome diferente.\n");
        return;
    }

    for (i = 0; i < MAX_REGISTROS; i++) {
        if (banco_dados[i][0] == '\0') {
            strcpy(banco_dados[i], nome);
            printf("Nome cadastrado com sucesso!\n");
            return;
        }
    }
    printf("Banco de dados cheio!\n");
}

void buscarRegistro() {
    char nome[MAX_LETRAS];
    int posicao;
    printf("Digite o nome para buscar: ");
    scanf(" %29[^\n]", nome);

    posicao = buscarNome(nome);

    if (posicao != -1) {
        printf("Nome encontrado na linha %d.\n", posicao + 1);
    } else {
        printf("Nome nao encontrado.\n");
    }
}

void modificarNome() {
    char nomeAntigo[MAX_LETRAS];
    char nomeNovo[MAX_LETRAS];
    int posicao;
    printf("Digite o nome que deseja alterar: ");
    scanf(" %29[^\n]", nomeAntigo);

    posicao = buscarNome(nomeAntigo);

    if (posicao == -1) {
        printf("Nome nao encontrado.\n");
        return;
    }

    printf("Digite o novo nome: ");
    scanf(" %29[^\n]", nomeNovo);

    if (buscarNome(nomeNovo) != -1) {
        printf("Erro! Ja existe um registro com esse nome.\n");
        return;
    }

    strcpy(banco_dados[posicao], nomeNovo);
    printf("Nome alterado com sucesso!\n");
}

void apagarNome() {
    char nome[MAX_LETRAS];
    int posicao;
    printf("Digite o nome que deseja remover: ");
    scanf(" %29[^\n]", nome);

    posicao = buscarNome(nome);

    if (posicao == -1) {
        printf("Nome nao encontrado.\n");
        return;
    }

    banco_dados[posicao][0] = '\0';

    printf("Nome removido com sucesso!\n");
}

void mostarTodos() {
    int i;
    int encontrou = 0;
    printf("\nLISTA DE NOMES:\n");

    for (i = 0; i < MAX_REGISTROS; i++) {
        if (banco_dados[i][0] != '\0') {
            printf("Indice %d -> %s\n", i + 1, banco_dados[i]);
            encontrou = 1;
        }
    }

    if (!encontrou) {
        printf("Nenhum nome cadastrado.\n");
    }
}

int main() {
    int opcao;
    int i;
    for (i = 0; i < MAX_REGISTROS; i++) {
        banco_dados[i][0] = '\0';
    }

    do {
        printf("\n");
        printf("1 - Incluir\n");
        printf("2 - Buscar\n");
        printf("3 - Modificar\n");
        printf("4 - Apagar\n");
        printf("5 - Listar Todos\n");
        printf("0 - Sair\n");
        printf("Digite o número da opção que deseja escolher: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                addNome();
                break;

            case 2:
                buscarRegistro();
                break;

            case 3:
                modificarNome();
                break;

            case 4:
                apagarNome();
                break;

            case 5:
                mostarTodos();
                break;

            case 0:
                printf("Programa encerrado.\n");
                break;

            default:
                printf("Opção invalida!\n");
        }

    } while (opcao != 0);

    return 0;
}
