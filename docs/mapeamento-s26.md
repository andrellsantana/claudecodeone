# Mapeamento do S-26 (etapa 1)

Origem: PDF impresso pelo Chrome (Skia), A4 retrato, 3 páginas, **sem campos de formulário (AcroForm)**; todo o conteúdo é texto fixo.

## Página 2 – Quadro 1: Confronto Conta Bancária
| Item | Campo | Tipo | Regra |
|---|---|---|---|
| — | Data do preenchimento | data dd/mm/aaaa | entrada |
| 1 | Saldo final do extrato bancário | valor | entrada |
| 2 | Depósitos não no extrato (+) | valor | entrada |
| 3 | Taxas bancárias não registradas (+) | valor | entrada |
| 4 | Total dos itens 1 a 3 | valor | **1 + 2 + 3** |
| 5 | Transferências/cheques não processados (lista: N.º confirmação/cheque + Valor) | lista | entrada |
| 6 | Total do item 5 (–) | valor | **soma do item 5** |
| 7 | Juros bancários não registrados (–) | valor | entrada |
| 8 | Donativos eletrônicos não registrados | valor | entrada |
| 9 | Saldo após confronto | valor | **4 − 6 − 7 − 8**; deve = Resumo › CONTA › Total |

## Página 2 – Quadro 2: Confronto de Outra Conta (Fundos mantidos em Betel)
| Item | Campo | Tipo | Regra |
|---|---|---|---|
| — | Data do preenchimento | data | entrada |
| 1 | Saldo final do extrato | valor | entrada |
| 2 | Depósitos não no extrato (+) | valor | entrada |
| 3 | Taxas não registradas (+) | valor | entrada |
| 4 | Total dos itens 1 a 3 | valor | **1 + 2 + 3** |
| 5 | Saques não registrados (lista: Descrição + Valor) | lista | entrada |
| 6 | Total do item 5 (–) | valor | **soma do item 5** |
| 7 | Juros não registrados (–) | valor | entrada |
| 8 | Saldo após confronto | valor | **4 − 6 − 7**; deve = Resumo › OUTRA CONTA › Total |

## Página 3 – Resumo (somente leitura, para validação)
Blocos ENTRADAS, CONTA, OUTRA CONTA (cada um: saldo anterior, entrada, saída, Total) e SALDO DISPONÍVEL.
Os valores esperados são lidos de cada PDF carregado.
O mesmo valor também aparece no texto de instrução da página 2 ("deve ser igual a R$ …") – usado como conferência dupla.

## Achado importante: a posição muda entre PDFs
O PDF em branco e o preenchido têm **escalas e quebras de linha diferentes**.
Logo, coordenadas fixas não servem. A aplicação localizará as âncoras em cada PDF carregado:
- linha de cada item: marcador "N." na coluna do quadro;
- coluna dos valores: sinais "+" / "–" (valor alinhado à direita antes do sinal);
- tamanho da fonte: proporcional à fonte detectada no próprio PDF.
