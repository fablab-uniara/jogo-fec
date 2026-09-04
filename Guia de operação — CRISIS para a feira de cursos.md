# Guia de operação — CRISIS para a feira de cursos

## Arquivos da entrega

| Arquivo | Função |
|---|---|
| `crisis_feira.html` | Jogo exibido no monitor ou tablet do estande. |
| `perfil.html` | Página mobile aberta pelo QR Code após uma partida concluída. |
| `logo-uniara.png` | Logotipo opcional. Coloque-o na mesma pasta dos dois arquivos para a marca aparecer. |

## O que foi implementado

A versão de feira reduz a rodada para **45 segundos e três decisões**. O desafio inicia com métricas equilibradas, sinaliza claramente a decisão atual (`1/3`, `2/3` e `3/3`) e registra as competências relacionadas a cada cenário.

A tela final só gera um perfil quando a pessoa conclui ao menos duas decisões. Caso o tempo termine antes disso, o resultado passa a ser **“Missão interrompida”**, sem perfil positivo e sem QR Code. Isso evita que uma partida sem interação pareça uma vitória.

Ao concluir a rodada, o visitante recebe um dos quatro perfis: **Líder de Pessoas**, **Estrategista de Crescimento**, **Guardião Financeiro** ou **Inovador de Negócios**. O QR Code conduz a `perfil.html`, que exibe o resultado no celular, apresenta as competências observadas e direciona para a página do curso de Administração da UNIARA.

Após a conclusão, a tela de resultado permanece aberta indefinidamente para que o visitante possa escanear o QR Code com calma. A nova rodada só começa quando alguém clica em `JOGAR NOVAMENTE`; não existe retorno automático. O toque é o modo principal de interação; a câmera com gesto de pinça continua disponível como recurso adicional.

A camada dramática agora comunica a consequência de cada escolha em tempo real. Depois de uma decisão, o jogo exibe um alerta contextual com o efeito nos indicadores, atualiza o status da operação e pode disparar mensagens como `ALERTA: DECISÃO AGRAVOU A CRISE`, `EMPRESA EM APUROS`, `SINAL DE RECUPERAÇÃO` ou `A empresa ganhou fôlego.`. O cronômetro também gera avisos progressivos aos 15, 10 e 5 segundos para aumentar a urgência sem mudar a estrutura de três decisões.

Os alertas foram desenhados como intervenções centrais: o fundo escurece e ganha textura, o jogo ao fundo é desfocado, a mensagem aparece ampliada no centro da tela e uma barra inferior acompanha o tempo de leitura. Após a redução solicitada, o alerta inicial permanece por aproximadamente 9 segundos; as consequências comuns permanecem por aproximadamente 7 segundos; estados de perigo permanecem por aproximadamente 9 segundos; e o resultado final permanece por aproximadamente 11 segundos. Durante a mensagem, os botões ficam temporariamente bloqueados e o cronômetro pausa para que o visitante consiga ler antes de continuar. Alertas de perigo também recebem pulsação visual e sinal sonoro dedicado.

A tela final ganhou um balanço narrativo explícito. Em resultados fortes, o visitante vê `EMPRESA SALVA` e `VOCÊ SALVOU A EMPRESA.`; em resultados intermediários, recebe uma leitura de sobrevivência ou alerta de continuidade; em resultados insuficientes, a experiência informa colapso operacional ou missão interrompida. O bloco `SUAS DECISÕES DE COMANDO` registra cada escolha, competência observada e leitura de impacto, preservando o QR Code e o fluxo de perfil quando a partida é concluída.

## Publicação correta

Publique `crisis_feira.html` e `perfil.html` no **mesmo diretório** de um servidor web público. A página principal poderá ter qualquer nome, mas a página de perfil precisa continuar com o nome `perfil.html`, a menos que você também altere a constante `PROFILE_LANDING_PAGE` no jogo.

Quando o jogo é aberto diretamente como arquivo local (`file://`), o QR Code usa a página pública do curso como contingência. Depois de publicado em endereço `https://`, ele passa a apontar automaticamente para `perfil.html` na mesma pasta, com perfil, pontuação e parâmetros de campanha. Essa regra permite testar o jogo offline sem gerar um QR Code com endereço de arquivo local.

> Para usar a câmera, publique via **HTTPS** e conceda permissão quando o navegador solicitar. O jogo continua funcional por toque se a câmera não estiver disponível.

## Preparação antes de abrir o stand

| Etapa | Verificação |
|---|---|
| Arquivos | `crisis_feira.html`, `perfil.html` e, se desejado, `logo-uniara.png` estão na mesma pasta publicada. |
| Link | O QR Code de uma partida concluída abre a página de perfil no celular e o botão final abre a página do curso. |
| Hardware | Teste toque, cabo de energia, resolução em modo paisagem, som e conexão. |
| Navegador | Abra em tela cheia. O duplo clique também solicita tela cheia quando permitido. |
| Câmera | Trate-a como opcional: faça uma rodada inteira somente por toque. |
| QR Code e retorno | Confirme que o QR Code permanece visível sem limite de tempo e que a abertura só retorna após clicar em `JOGAR NOVAMENTE`. |
| Impacto | Faça uma rodada com decisões difíceis e confirme os alertas centrais ampliados, status `EMPRESA EM APUROS` e resumo final das decisões. Aguarde a mensagem desaparecer antes de tentar a próxima escolha; o cronômetro deve permanecer pausado durante a leitura. |

## Ajustes rápidos no código

As principais configurações ficam próximas ao início do JavaScript de `crisis_feira.html`.

```js
const ROUND_SECONDS = 45;
const ROUND_SCENARIOS = 3;
const MIN_DECISIONS_FOR_PROFILE = 2;
const BASE_METRICS = { cash: 75, moral: 75, market: 70, risk: 25 };
```

Você pode ajustar tempo, quantidade de decisões e dificuldade alterando esses valores. Para preservar a experiência de feira, mantenha a partida entre 30 e 60 segundos e evite mais de quatro decisões.

## Itens não incluídos nesta versão

Esta entrega não coleta dados pessoais, não possui ranking compartilhado e não grava métricas em servidor. Isso foi intencional: a versão pode ser publicada como página estática, sem expor dados de visitantes no dispositivo do estande.

A próxima etapa recomendada, se a UNIARA quiser captar contatos, é criar uma página de continuação com formulário opcional no celular do visitante e um painel restrito para a equipe. Antes de coletar dados, o texto de finalidade, o consentimento e o fluxo para possíveis participantes menores devem ser aprovados pela área institucional de privacidade e pela orientação jurídica responsável.
