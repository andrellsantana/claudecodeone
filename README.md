# Confrontos S-26

Aplicação web para preencher os quadros de confronto da página 2 da Folha de Contas (S-26) e gerar o PDF já preenchido.

**Acesse:** https://andrellsantana.github.io/confrontoss26/

Funciona no celular e no computador, sem instalação e sem cadastro. O PDF é processado no próprio aparelho e não é enviado para nenhum servidor.

## Como usar

1. Abra o link e carregue o S-26 em PDF, com os quadros de confronto ainda em branco.
2. Preencha os dois quadros:
   - **Confronto: conta bancária** (itens 1 a 9)
   - **Confronto: outra conta, fundos mantidos em Betel** (itens 1 a 8)
3. Os totais são calculados enquanto você digita. Abaixo de cada quadro aparece se o saldo confere com o Resumo.
4. Quando os dois saldos conferirem, toque em **Gerar PDF preenchido**. No celular, o botão **Compartilhar** permite enviar o arquivo direto pelo WhatsApp.

## Regras

| Quadro | Totais calculados | Validação |
|---|---|---|
| Conta bancária | 4 = 1 + 2 + 3 · 6 = soma do item 5 · 9 = 4 − 6 − 7 − 8 | Item 9 = Total de **Conta** no Resumo (página 3) |
| Outra conta | 4 = 1 + 2 + 3 · 6 = soma do item 5 · 8 = 4 − 6 − 7 | Item 8 = Total de **Outra conta** no Resumo (página 3) |

- O PDF só é gerado se as duas validações conferirem e as datas forem válidas.
- O item 5 aceita até 7 linhas. Cada linha usada precisa de descrição (ou N.º) e valor.
- PDFs com os quadros já preenchidos são recusados.
- Formato brasileiro: datas em dd/mm/aaaa e valores como 1.234,56, sem símbolo de moeda. Para digitar um valor, use só números: 458850 vira 4.588,50.
- A data do preenchimento vem com a data de hoje e pode ser alterada.

## Como funciona o alinhamento

A posição dos campos muda de um PDF para outro, conforme a impressão. Por isso a aplicação não usa coordenadas fixas. Em cada PDF carregado, ela localiza:

- os números dos itens e o fim de cada rótulo, para definir a linha de cada valor;
- os sinais **+** e **–**, para definir a coluna dos valores, alinhados à direita;
- as linhas desenhadas da tabela do item 5;
- o tamanho da letra do formulário.

Os valores são escritos em Helvetica, fonte com as mesmas medidas da Arial.

O S-26 deve ser salvo pelo Chrome com **Imprimir → Salvar como PDF**, em A4, retrato, margens padrão e escala 100%.

## Estrutura do projeto

| Arquivo | Conteúdo |
|---|---|
| `index.html` | A aplicação completa: tela, cálculos, leitura e geração do PDF |
| `vendor/` | Bibliotecas [pdf.js](https://mozilla.github.io/pdf.js/) 3.11.174 (leitura) e [pdf-lib](https://pdf-lib.js.org/) 1.17.1 (escrita), incluídas localmente |
| `docs/mapeamento-s26.md` | Mapeamento dos campos do S-26 |

## Publicação

A aplicação é publicada pelo GitHub Pages a partir da branch `main`, pasta raiz. Toda alteração enviada à `main` entra no ar em um ou dois minutos.

Para testar no computador, sirva a pasta com um servidor local, porque o leitor de PDF não funciona abrindo o arquivo direto:

```bash
python3 -m http.server 8000
```

Depois abra http://localhost:8000.

> **Atenção:** este repositório é público. Não envie PDFs com dados reais para ele.
