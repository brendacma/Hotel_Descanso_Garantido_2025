# Especificação do Sistema – Hotel Descanso Garantido (Versão Reduzida – 4 Funcionalidades)

## 1. Visão Geral

Este documento descreve a especificação do sistema a ser desenvolvido como parte do Trabalho Interdisciplinar de Fundamentos de Engenharia de Software. Como o aluno não está matriculado em Algoritmos e Estruturas de Dados I, esta versão reduzida contempla apenas quatro funcionalidades do sistema original:

1. Cadastro de Clientes  
2. Cadastro de Funcionários  
3. Cadastro de Quartos  
4. Cadastro de Estadias

O sistema deverá apresentar um menu simples, operado via terminal, permitindo o acesso às funções acima. A entrega inclui código, documentação e planejamento.

---

## 2. Escopo do Sistema

O sistema deve permitir o registro de informações essenciais do hotel, garantindo integridade, consistência e validação das entradas. Os dados deverão ser armazenados de forma persistente.

> **Observação sobre linguagem e persistência (adaptação para C++):**  
> A especificação original da disciplina AED I exigia que “as informações manipuladas neste trabalho deverão ser armazenadas em arquivo(s) de acesso direto, utilizando bibliotecas em C”. Para esta versão reduzida (Fundamentos), você pode implementar o sistema em **C++**. **Mantém-se obrigatória a exigência de acesso direto a arquivos** (persistência por leitura/escrita em arquivos), porém a implementação deve usar recursos idiomáticos de C++:
> 
> - usar `#include <fstream>` e classes `std::fstream`, `std::ifstream`, `std::ofstream`;  
> - abrir arquivos em **modo binário** (`std::ios::binary`) para leitura/escrita de registros;  
> - suportar **acesso direto** usando `seekg` e `seekp` para posicionamento (leitura/escrita em posições específicas do arquivo);  
> - armazenar registros em formato de tamanho fixo (por exemplo, `struct` com campos de tamanho fixo ou com padding controlado), ou implementar uma estratégia clara de serialização/deserialização (ex.: escrever comprimentos + bytes em sequência) que permita localizar/atualizar registros sem carregar todo o arquivo na memória;  
> - ao usar classes/objetos, atente para conversão para blocos binários (por exemplo, criar funções `serialize()` / `deserialize()` que escrevam/leiam campos primitivos e strings de tamanho controlado);  
> - documentar claramente o formato do arquivo e a estratégia de acesso direto no `.md`.
>
> **Importante:** se o professor de AED I requisitar estritamente o uso de C puro, você deverá seguir a especificação original em C. Nesta versão para FES, C++ é permitido, desde que a persistência por acesso direto seja respeitada.

---

## 3. Requisitos Funcionais (RF)

### RF01 – Cadastrar Cliente
O sistema deve permitir o cadastro de clientes, armazenando:
- código do cliente (único; pode ser criado automaticamente)  
- nome  
- endereço  
- telefone

Regras:
- Não pode haver dois clientes com o mesmo código.  
- Validar duplicidade antes de salvar.  
- Mensagens claras de sucesso/erro.

### RF02 – Cadastrar Funcionário
O sistema deve permitir o registro de funcionários, contendo:
- código (único; pode ser criado automaticamente)  
- nome  
- telefone  
- cargo  
- salário

Regras:
- Impedir duplicidade de código.  
- Validar antes do salvamento.

### RF03 – Cadastrar Quarto
O sistema deve permitir cadastrar quartos com os campos:
- número do quarto (único)  
- quantidade máxima de hóspedes  
- valor da diária  
- status (inicialmente sempre “desocupado”)

Regras:
- Não aceitar dois quartos com o mesmo número.  
- Status inicial = “desocupado”.

### RF04 – Cadastrar Estadia
Para cadastrar uma estadia, o usuário fornecerá:
- código do cliente (deve existir)  
- quantidade de hóspedes  
- data de entrada  
- data de saída

O sistema deverá:
1. verificar existência do cliente;  
2. localizar um quarto que esteja cadastrado, **desocupado** e com capacidade adequada;  
3. calcular quantidade de diárias (ver regras abaixo);  
4. criar registro de estadia contendo: código da estadia, datas, diárias, código do cliente, número do quarto;  
5. atualizar status do quarto para “ocupado”.

Regras adicionais:
- Não cadastrar estadia em quarto ocupado.  
- Não aceitar datas inválidas ou invertidas.  
- Calcular diárias considerando check-in às 14h e check-out às 12h do dia seguinte.

---

## 4. Requisitos Não Funcionais (RNF)

- **Persistência:** os dados devem ser persistidos em arquivos no disco, conforme a seção de observação sobre C++.  
- **Interface:** menu textual via terminal.  
- **Modularidade:** cada operação em função/módulo separado.  
- **Organização:** código comentado, organizado em arquivos fonte e headers quando aplicável.  
- **Documentação:** toda função/documento em `.md`.

---

## 5. Estratégia de Arquivos e Acesso Direto em C++

1. **Formato de Registro:** usar registros de tamanho fixo ou serialização manual.  
2. **Serialização/Deserialização:** implementar funções dedicadas para escrita/leitura binária.  
3. **Abertura de Arquivo:** usar `std::fstream` em modo binário.  
4. **Posicionamento:** usar `seekg`/`seekp` para acessar diretamente posições específicas.  
5. **Atualizações:** sobrescrever registros diretamente por offset.  
6. **Leitura/Verificação:** buscar registros sequencialmente ou por índice simples.  
7. **Backup:** manter cópias dos arquivos durante o desenvolvimento.

---

## 6. Estrutura da Função main

O menu deve conter:
1. Cadastrar Cliente  
2. Cadastrar Funcionário  
3. Cadastrar Quarto  
4. Cadastrar Estadia  
5. Sair

O menu deve permanecer em loop até a opção "Sair".

---

## 7. Documentação das Funções (.md)

Cada função deve incluir:
- Nome da função  
- Propósito  
- Entradas  
- Saída  
- Validações  
- Pré e pós-condições  
- Possíveis erros  
- Exemplo de uso

---

## 8. Planejamento (Backlog / Scrum)

Mesmo individualmente, incluir:
- Backlog priorizado dos quatro requisitos  
- Sprints de 3–4 dias  
- Evolução do backlog  
- Registro das atividades realizadas

---

## 9. Testes

Para cada módulo:
- Descrever casos de teste (entrada, procedimento, saída esperada).  
- Executar manualmente.  
- Criar relatório de aprovação/reprovação.

---

## 10. Entregáveis

1. Código fonte em C++  
2. Documentação em `.md`  
3. Backlog + sprints  
4. Planejamento e relatório de testes  
5. Arquivos de dados (se usados)  
6. Vídeo de apresentação

---

## 11. Observações Finais

- A adaptação para C++ não remove a exigência de acesso direto a arquivos.  
- Se a coordenação exigir C puro, o código deve seguir a versão original.  
- Documentar no `.md` o formato binário adotado e como é feito o acesso direto.