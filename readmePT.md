# Google AI Pro (5 TB) — Dois anos sem custo

Painel totalmente automatizado para US$0,00 → 24 meses.

[English](README.md)

## Requisitos do sistema

1. Windows 10 ou 11.
2. Google Chrome instalado no caminho padrão.
3. Python 3.10 ou superior instalado com a opção **Add Python to PATH** marcada.
4. Um proxy dos Estados Unidos (US) ativado no computador, ou um modelo de proxy preenchido no lado esquerdo do painel.

## Início rápido

1. No primeiro uso, dê dois cliques em `1_首次运行_安装依赖并启动.bat` para instalar as dependências e iniciar o painel.
2. Nos próximos usos, dê dois cliques em `2_启动控制台.bat`.
3. O navegador abrirá automaticamente o painel em http://127.0.0.1:8765.

## Configuração do cartão e das contas

### Informar um cartão de pagamento (obrigatório)

Na seção **Configuração global e cadastro integrado de cartão com isenção de impostos**, à esquerda, informe seu próprio cartão Visa ou Mastercard habilitado para pagamentos em moeda estrangeira:

- Número do cartão (16 dígitos).
- Mês e ano de validade, como `08 / 29`.
- Código de segurança (CVC de 3 dígitos).
- Nome do titular em inglês.
- O código postal para isenção de impostos vem preenchido como `97201` (Oregon, Estados Unidos); as instruções originais indicam que não é necessário alterá-lo.

Clique em **💾 Salvar configuração**.

Segundo a documentação original, o script inclui uma proteção rigorosa de custo zero e só clica em Assinar quando a janela de pagamento confirma **US$0,00**, sem cobranças durante o processo.

### Importar contas Google em lote

Cole as contas na seção **Importação de contas em lote**, à direita, com uma conta por linha. Os formatos aceitos são:

```text
email----senha----email_de_recuperacao
email----senha----email_de_recuperacao----chave_2FA
email----senha----chave_2FA
```

Clique em **➕ Importar lista de contas**.

### Iniciar a execução automática

Clique em **▶ Executar** ao lado de uma conta ou em **▶ Executar todas automaticamente** na parte superior.

O script foi projetado para realizar automaticamente estas etapas:

1. Entrar no Google e concluir a verificação por e-mail de recuperação ou 2FA.
2. Cadastrar o cartão de forma integrada com isenção de impostos e ativar o primeiro pacote gratuito de 12 meses (US$0,00).
3. Acumular um segundo pacote gratuito de 6 meses (US$0,00 → 18 meses).
4. Acumular um terceiro pacote gratuito de 6 meses (US$0,00 → limite de 24 meses).
5. Abrir o Google Play, cancelar a renovação automática para manter o benefício de dois anos até o vencimento e capturar uma tela para comprovação.

## Links originais

- Loja de cartões: https://faka.cdkey.si
- Blog: https://blog.caowo.de
- Grupo no Telegram: @Hello_Florence
