# Provisões Centralização

Ferramenta em um único arquivo HTML que confere a **Centralização** com o **SF1** e gera as provisões do mês
(só despesa, pelo valor líquido, com sinal negativo e sem contrapartida de passivo).

Tudo roda no navegador: nenhum arquivo é enviado para fora do computador.

## Como usar

1. Abra `index.html` no Chrome ou no Edge (precisa de internet para carregar a fonte e a biblioteca de Excel).
2. Escolha o mês e o ano.
3. Solte os arquivos (todos de uma vez, se quiser):
   - Centralização do mês (`.xlsx`) e SF1 do mês (`.csv`): obrigatórios.
   - Analise da Base (`.xlsb`): opcional, confere se a NF já está na base como provisão do mês ou lançamento do razão.
   - Cadastro de fornecedor SA2 (`.csv`): opcional, confere código e CNPJ de cada NF.
4. Confira os indicadores e as abas, trate as pendências e baixe o Excel.

O passo a passo completo está no botão **POP resumido**, dentro da própria página.

## O que a ferramenta faz

- Valida as abas ENERGIA, BENEFICIOS, REFEIÇÃO, TI-SISTEMA-INFRA, VIAGENS, IMÓVEIS e FACILITIES contra o SF1
  (chave: Filial + NF + Fornecedor).
- Gera as provisões das NFs não lançadas, com conta contábil, filial e centro de custo.
- Separa o que precisa de validação: já na base, sem conta, não provisionadas por regra, filiais a cadastrar,
  fornecedores com código ou CNPJ divergente e alertas de valor divergente ou NF duplicada.
- Exporta tudo em um Excel (linhas 05 PENDENTE PGTO e 06 PGTO REALIZADO em amarelo e negrito).

## Regras de negócio embutidas

- Centro de custo que começa com 03 (CAPEX) e item CONV FARMACIA do fornecedor GOLDEN FARMA não são provisionados.
- Imóveis: só entram CONDOMINIO e AGUA/ESGOTO (os demais itens são IFRS 16).
- Viagens: LOCAÇÃO FROTA fica fora (IFRS 16); na filial 001011 o centro de custo é 01060110026.
- Facilities: centro de custo por item (limpeza, vigilância e portaria em 02070400014; mão de obra em 02070410026).
- Energia: centro de custo 01 vai para 01020070001; filiais 010001 a 010004 para 02180410031; demais para 02070410026.

## Manutenção

- O arquivo é autocontido. Os catálogos (contas, centros de custo, unidades e de-para de itens), os logos e as regras
  estão dentro do HTML. Mudou uma conta, um centro de custo, uma filial ou um item? Atualize o catálogo embutido
  ou solte o arquivo de catálogo correspondente na página.
- Dependências carregadas da internet: biblioteca de Excel `xlsx-js-style` (jsDelivr) e a fonte Montserrat (Google Fonts).
- Conteúdo interno da empresa (catálogos e marca): manter o repositório **privado**.