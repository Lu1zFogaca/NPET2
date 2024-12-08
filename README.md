#include <stdio.h>

int main() {
  char doacao[20], tipo_fis[30], nome[30], tipo_cart[20];
  float valor, parcelado;
  int parcelas, dia, mes, ano, opcao, tipo_pagamento, tipo_cartao;

  printf("\nPara qual instituição você deseja doar? ");
  fgets(nome, sizeof(nome), stdin); 
  nome[strcspn(nome, "\n")] = '\0';

  do {
    printf("\nEscolha o tipo de doação:\n");
    printf("1. Produto\n");
    printf("2. Monetária\n");
    printf("Digite o número da sua escolha: ");
    scanf("%d", &opcao);

    if (opcao == 1 || opcao == 2) {
      break;
    } else {
      printf("\nOpção inválida. Por favor, escolha entre 1 ou 2.\n");
    }
  } while (1);

  if (opcao == 1) {
    do {
      printf("\nQual tipo de produto você gostaria de doar? (Alimentos, Medicamentos, Brinquedos ou Cobertores): ");
      scanf("%19s", tipo_fis);

      if (strcmp(tipo_fis, "Alimentos") == 0 ||
          strcmp(tipo_fis, "alimentos") == 0 ||
          strcmp(tipo_fis, "Medicamentos") == 0 ||
          strcmp(tipo_fis, "medicamentos") == 0 ||
          strcmp(tipo_fis, "Brinquedos") == 0 ||
          strcmp(tipo_fis, "brinquedos") == 0 ||
          strcmp(tipo_fis, "Cobertores") == 0 ||
          strcmp(tipo_fis, "cobertores") == 0) {
        break;
      } else {
        printf("\nTipo de produto inválido. Escolha entre Alimentos, Medicamentos, Brinquedos ou Cobertores.\n");
      }
    } while (1);

    do {
      printf("\nQuando você deseja agendar a visita? Por favor, informe o dia, mês e ano, separados por espaço (exemplo: 30 9 2024): ");
      scanf("%d %d %d", &dia, &mes, &ano);

      if (dia > 31 || dia < 1 || 
          (dia == 31 && mes == 2) || (dia == 31 && mes == 4) ||
          (dia == 31 && mes == 6) || (dia == 31 && mes == 9) ||
          (dia == 31 && mes == 11) || (dia == 29 && mes == 2 && ano % 4 != 0) ||
          (dia == 30 && mes == 2)) {
        printf("\nData inválida. Por favor, informe uma data válida.\n");
      } else if (mes > 12 || mes < 1) {
        printf("\nData inválida. Por favor, informe um mês válido.\n");
      } else {
        printf("\nUma visita foi agendada para a instituição %s, no dia %d do %d de %d, a fim de doar %s. Muito obrigado pela doação!\n", nome, dia, mes, ano, tipo_fis);
        break;
      }
    } while (1);
  } else if (opcao == 2) {
    printf("\nQuanto você gostaria de doar, em reais? ");
    scanf("%f", &valor);

    do {
      printf("\nEscolha a forma de pagamento:\n");
      printf("1. Cartão\n");
      printf("2. PIX\n");
      printf("3. TED\n");
      printf("Digite o número da sua escolha: ");
      scanf("%d", &tipo_pagamento);

      if (tipo_pagamento == 1 || tipo_pagamento == 2 || tipo_pagamento == 3) {
        break;
      } else {
        printf("\nOpção inválida. Escolha entre 1, 2 ou 3.\n");
      }
    } while (1);

    if (tipo_pagamento == 1) {
      do {
        printf("\nVocê gostaria de pagar com qual tipo de cartão?\n");
        printf("1. Crédito\n");
        printf("2. Débito\n");
        printf("Digite o número da sua escolha: ");
        scanf("%d", &tipo_cartao);

        if (tipo_cartao == 1 || tipo_cartao == 2) {
          break;
        } else {
          printf("\nOpção inválida. Escolha entre 1 (Crédito) ou 2 (Débito).\n");
        }
      } while (1);

      if (tipo_cartao == 1) {

        
        do {
          printf("\nEm quantas vezes você deseja parcelar (escolha entre 1 a 6 parcelas)? ");
          scanf("%d", &parcelas);
          parcelado = valor / parcelas;

          if (parcelas >= 1 && parcelas <= 6) {
            printf("\nUma doação de R$%.2f será feita usando cartão de crédito, em %d parcelas de R$%.2f sem juros, para a instituição %s. Muito obrigado!\n", valor, parcelas, parcelado, nome);
            break;
          } else {
            printf("\nNúmero de parcelas inválido. Escolha entre 1 e 6 parcelas.\n");
          }
        } while (1);
      } else if (tipo_cartao == 2) {
        printf("\nUma doação de R$%.2f será feita usando cartão de débito para a instituição %s. Muito obrigado!\n", valor, nome);
      }
    } else if (tipo_pagamento == 2 || tipo_pagamento == 3) {
      if (tipo_pagamento == 2) {
        printf("\nObrigado pela doação de R$%.2f via PIX para %s!\n", valor, nome);
      } else if (tipo_pagamento == 3) {
        printf("\nObrigado pela doação de R$%.2f via TED para %s!\n", valor, nome);
      }
    }
  }

  return 0;
}
