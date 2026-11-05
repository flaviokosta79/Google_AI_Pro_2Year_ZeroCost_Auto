# Google AI Pro (5 TB) — Dois anos sem custo

Painel totalmente automatizado para US$0,00 → 24 meses.

[English](README.md)

## O que a aplicação faz de ponta a ponta

A aplicação combina um painel local em FastAPI (`app.py`) com um motor de automação de navegador em Playwright (`automation_engine.py`). Seu objetivo é ativar e acumular ofertas promocionais do Google AI, depois cancelar opcionalmente a renovação automática e registrar o estado da assinatura.

1. **Configurar a sessão.** O painel salva a região de destino, o plano, a preferência de cancelamento da renovação automática, o modelo de proxy e o cartão em `config.json`.
2. **Carregar as contas.** Importe as credenciais Google, opcionalmente com e-mail de recuperação, chave TOTP e proxy específico por conta. Contas existentes são atualizadas quando o e-mail normalizado corresponde. Contas novas entram na fila como pendentes.
3. **Escolher a execução.** Execute uma conta ou um lote sequencial. O backend também aceita uma etapa inicial para pular fases anteriores. O painel apresenta logs, etapa atual, estado e capturas de tela; permite redefinir ou remover contas, e os pedidos de parada são verificados entre as etapas do fluxo.
4. **Preparar um perfil de navegador isolado.** O motor valida os campos obrigatórios do cartão, abre o Chrome com um perfil persistente por conta, conecta pelo Playwright e aplica o proxy selecionado, quando configurado. Tenta identificar o IP de saída e o país do navegador antes de continuar.
5. **Entrar na conta.** O motor preenche o login Google e tenta resolver os desafios compatíveis de e-mail de recuperação, senha e TOTP usando os dados importados.
6. **Tentar a sequência promocional.** Consulta as assinaturas no Google Play e tenta uma oferta de 12 meses seguida por duas de 6 meses, visando 24 meses no total. Os dados das ofertas também incluem um adicional de teste do YouTube Premium. O código modifica requisições da página do Google One com identificadores de oferta embutidos, preenche o cartão e procura um valor de custo zero no texto da janela de pagamento. Usa informações da assinatura existente para pular algumas etapas e repete certas tentativas de contratação.
7. **Tratar a renovação e coletar evidências.** Se o cancelamento automático estiver habilitado, tenta cancelar a renovação no Google Play. Depois consulta novamente as assinaturas, captura uma tela final, extrai a data de vencimento quando reconhecida e registra o plano detectado e o estado de conclusão.
8. **Manter o resultado disponível.** Atualizações das contas e resultados são gravados em `config.json`; perfis do navegador permanecem em `profiles/` e capturas em `screenshots/`. Os logs de execução ficam em memória. Exceções tratadas pelo fluxo são registradas como erros da conta.

### Escopo e limitações atuais

Esta descrição corresponde ao fluxo implementado, sem comprovar a concessão do benefício ou garantir gratuidade. Disponibilidade das ofertas, elegibilidade, comportamento do pagamento e vencimento final dependem do Google. O script contém verificações fixas de datas de 2027/2028 e seletores de texto das páginas; por isso, o estado de conclusão e as capturas devem ser conferidos na página real da assinatura.

O fluxo completo de navegador atualmente depende do Windows: a localização do Chrome e os comandos de gerenciamento de processos são específicos desse sistema. Na preparação do ambiente na nuvem, foram validados apenas a instalação das dependências e o painel/API no Linux; login Google, contratação, acúmulo de ofertas e cancelamento não foram executados.

## Requisitos do sistema

1. Windows 10 ou 11.
2. Google Chrome instalado no caminho padrão.
3. Python 3.10 ou superior instalado com a opção **Add Python to PATH** marcada.
4. Um proxy dos Estados Unidos (US) ativado no computador, ou um modelo de proxy preenchido no lado esquerdo do painel.

## Início rápido

1. No primeiro uso, dê dois cliques em `1_install_dependencies_and_start.bat` para instalar as dependências e iniciar o painel.
2. Nos próximos usos, dê dois cliques em `2_start_dashboard.bat`.
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
