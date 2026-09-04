# Validação da versão de feira

A tela inicial carregou com a chamada de três decisões em 45 segundos. Após iniciar, a primeira tela exibiu métricas iniciais ajustadas, cronômetro de 45 segundos e o indicador `DECISÃO 1/3` acompanhado da competência correspondente.

Duas escolhas sucessivas avançaram corretamente de `DECISÃO 1/3` para `DECISÃO 2/3` e `DECISÃO 3/3`. As métricas foram atualizadas a cada escolha e o cronômetro permaneceu ativo durante a rodada.

A terceira escolha encerrou a partida e exibiu `SEU PERFIL`, o balanço com `3/3` decisões, o perfil `LÍDER DE PESSOAS`, a chamada de escaneamento e o QR Code. A página `perfil.html` também foi validada com parâmetros de perfil, pontuação e competências; ela apresentou o conteúdo correto e preservou os parâmetros de campanha no link para o curso.

O encerramento sem decisões foi acionado para testar a regra de partida incompleta.

Após um ajuste de robustez, foi repetido o encerramento sem decisões para confirmar que a tela inicial é ocultada antes de a tela final aparecer.

O temporizador de inatividade foi acionado com atraso reduzido durante o teste da versão anterior para validar o retorno automático ao modo de atração.

A validação final de sintaxe JavaScript foi concluída sem erros para `crisis_feira.html` e `perfil.html`. O retorno automático por inatividade foi confirmado na versão anterior; na versão atual, a tela final permanece aberta até o reinício manual.


## Validação da camada dramática

A versão aprimorada manteve os 45 segundos, as três decisões, o uso opcional da câmera e o QR Code condicionado à conclusão suficiente. Na versão atual, a tela final permanece aberta indefinidamente após a partida, garantindo tempo para escanear o QR Code; somente `JOGAR NOVAMENTE` inicia outra rodada. Após o início, a interface apresentou o comunicado da diretoria e o status `OPERAÇÃO INSTÁVEL`.

Uma decisão de alto impacto exibiu um alerta com título, explicação e variação de caixa, moral, mercado e risco. Em uma sequência desfavorável, o jogo também apresentou `ALERTA: DECISÃO AGRAVOU A CRISE` e `ALERTA: EMPRESA EM APUROS`, enquanto o HUD refletia o risco elevado.

A tela final foi ampliada com `EMPRESA SALVA`, `VOCÊ SALVOU A EMPRESA.`, classificações de sobrevivência ou colapso, índice de comando, status final e o bloco `SUAS DECISÕES DE COMANDO`. Uma simulação positiva controlada confirmou a presença do resumo de três decisões, a geração do QR Code e a rolagem interna para telas menores.

A sintaxe dos JavaScripts embutidos em `crisis_feira.html`, `index.html` e `perfil.html` foi conferida sem erros após a sincronização das entradas principais.


## Ajuste de legibilidade dos alertas

Os alertas passaram a aparecer no centro da tela, com o restante da interface escurecido, texturizado e desfocado visualmente. A caixa de mensagem foi ampliada, o texto foi aumentado, a moldura ganhou pulsação nos estados críticos e a barra inferior acompanha o tempo real de exibição. Após a redução solicitada, o alerta inicial dura aproximadamente 9 segundos; as consequências comuns duram aproximadamente 7 segundos; estados críticos duram aproximadamente 9 segundos; e o resultado final dura aproximadamente 11 segundos. O cronômetro pausa enquanto o alerta está aberto.
