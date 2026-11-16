# COGI
## Documentação funcional

**Desenvolvido por Guilherme Augusto Barreta**

O COGI é um jogo de cartas 1×1 em que os jogadores usam componentes para gerar recursos, conjuram cartas do Extra Deck e disputam janelas de prioridade para responder às jogadas. O aplicativo reúne o menu principal, o construtor de decks, o tabuleiro e o lobby multiplayer.

## 1. Menu principal

| Opção | O que abre |
|---|---|
| **Jogar** | Seleção dos decks e do modo de partida contra a máquina ou de teste local. |
| **Montar deck** | Construtor para selecionar cartas do catálogo e salvar um deck. |
| **Multiplayer LAN** | Lobby para hospedar ou entrar em partidas pela rede local, VPN ou WebRTC, conforme a versão instalada. |
| **Exit** | Encerra o aplicativo. |

O menu identifica o desenvolvedor e apresenta um QR Code de contribuição voluntária. O jogo é gratuito.

## 2. Preparação dos decks

Cada jogador usa um **Deck Principal** para os componentes e um **Extra Deck** para as conjurações. Cada um desses baralhos aceita até **40 cartas**. O limite é de **5 cópias por carta**.

No construtor, selecione as cartas e suas quantidades e salve o deck em formato TXT. O mesmo arquivo pode ser importado na seleção de partidas e no lobby multiplayer. No ambiente de desenvolvimento, a pasta padrão do jogo é `code/meus-decks`. Se os decks não aparecerem automaticamente, use **Trocar pasta de decks**. No lobby, o seletor **Seu deck (.txt)** abre o arquivo diretamente.

## 3. Modos de jogo

| Modo | Comportamento |
|---|---|
| **Teste local** | Permite testar a interface, compras e movimentação no navegador. |
| **Usar servidor** | O motor valida as ações e o agente controla o oponente. Selecione um deck para cada lado. |
| **Multiplayer** | Cada participante escolhe seu próprio deck. O motor do anfitrião valida as jogadas dos dois jogadores. |

Na partida com motor, os jogadores começam com **100 pontos de vida** e **8 cartas na mão**. No multiplayer, o servidor sorteia quem recebe o primeiro turno e a prioridade inicial ao completar a sala. A mão adversária aparece pelo verso. O campo, os cemitérios, os contadores e o placar podem ser acompanhados no tabuleiro.

## 4. Turno, prioridade e pilha

No início do turno, os componentes e as conjurações viradas do dono do turno desviram. Quando um jogador toma uma ação que abre uma janela de resposta, a prioridade passa para o outro jogador. Uma resposta permite que a prioridade volte ao primeiro jogador. **Passar prioridade** cede a oportunidade de responder. **Encerrar turno** é uma decisão separada, tomada pelo dono do turno em uma janela apropriada.

Com **dois passes consecutivos**, os efeitos pendentes começam a resolver do mais recente para o mais antigo. Uma resposta nova reinicia a contagem de passes. Compras diretas e entradas de cartas sem efeito de resolução pendente produzem seu resultado imediato. Gatilhos de cartas entram na pilha e seguem o fluxo de resolução do motor. Quando a janela fecha, o dono do turno pode iniciar a batalha, se estiver disponível, ou encerrar o turno.

## 5. Recursos e conjuração

Baixe componentes da mão nos espaços do campo. Vire um componente elegível para acrescentar seu símbolo hermético à **reserva de recursos**. A **Pedra Filosofal** permite escolher o metal produzido. O **Colisor de Hádrons** é um exemplo de conjuração que pode produzir partículas, como Táquion.

Para conjurar, abra o Extra Deck, escolha uma carta habilitada e preencha os requisitos de custo e de campo dela. O custo consome os recursos correspondentes. Um requisito de presença de recurso, como o Táquion exigido pelo **Relógio Emissor de Táquion**, pode ser conferido sem consumir a partícula, conforme a regra da carta. As reservas são esvaziadas no fim do turno.

Ações em **instant speed** podem ser usadas em janelas permitidas durante a batalha. Uma ação instantânea admite respostas de conjuração ou de efeito instantâneo. Uma habilidade instantânea ativada exige virar sua carta, conforme a regra de ativação. Gatilhos automáticos continuam seguindo a resolução da pilha.

## 6. Batalha

1. O dono do turno inicia a batalha, seleciona os atacantes no campo e confirma os ataques.
2. Após a janela de respostas, o defensor escolhe no campo uma conjuração defensora e associa os ataques que ela vai bloquear. Ataques indefensáveis não recebem defensor.
3. Uma defensora pode bloquear vários ataques. Pode receber uma nova atribuição enquanto o total anterior estiver igual ou abaixo da resistência. Se a nova atribuição ultrapassar a resistência, ela pode ser aceita como o último bloqueio daquela defensora.
4. Na resolução, uma defensora vai ao cemitério se o ataque somado contra ela **superar** a resistência. Por exemplo, resistência 100 suporta 50 + 50. Ataques sem defesa atingem diretamente a vida do defensor.

As setas mostram as declarações de ataque e defesa e desaparecem ao encerrar o combate. Um atacante devolvido antes do dano deixa de contribuir para o combate. O **Rompimento de Barragem** interrompe os ataques em andamento ao entrar e bloqueia novas declarações naquele turno.

## 7. Exemplos de efeitos

| Carta | Comportamento |
|---|---|
| **Mago de Lorentz** | Entra em instant speed ao virar um Relógio válido. Na resolução do efeito, selecione os alvos no campo. Componentes retornam à mão e conjurações ao Extra Deck. |
| **Exponere** | Dá +10 de ataque aos seres que seu controlador controla enquanto estiver em campo. |
| **Guerreiro Laplaciano** | Ao resolver o gatilho de entrada, soma o ataque atual dos outros seres do seu lado. O próprio Guerreiro fica fora da soma. |
| **Moedor de Carne** | Ao resolver o efeito de entrada, o oponente compra uma carta e depois mói uma carta. Moer envia o topo do Deck Principal ao cemitério. |
| **Açougueiro Macabro** | A compra bem-sucedida de qualquer jogador faz o oponente do controlador moer uma carta. Sua habilidade instantânea vira o Açougueiro e, na resolução, faz esse oponente moer uma carta para cada carta no próprio cemitério. |

## 8. Encerramento da partida

- **Vida zero:** perde quem tiver a vida reduzida a zero.
- **Deckout:** perde quem tentar comprar com o Deck Principal vazio. Comprar ou moer a última carta deixa o deck vazio. A derrota ocorre na próxima tentativa de compra.

O painel de resultado cobre o tabuleiro e mostra **VOCÊ VENCEU** ou **VOCÊ PERDEU** da perspectiva de quem está jogando. A indicação abaixo da mensagem mostra o motivo do encerramento.

## 9. Multiplayer

### Rede local ou VPN

1. O anfitrião abre **Multiplayer**, seleciona **Rede local / VPN**, escolhe a interface de rede e o deck e cria a sala.
2. Ele envia ao convidado o **IPv4 selecionado** e o **código da sala**.
3. O convidado escolhe **Entrar por código**, informa os dados e seleciona o próprio deck.
4. Com os dois jogadores conectados, cada um clica em **Abrir tabuleiro**.

Na mesma rede local, use o IPv4 do anfitrião naquela rede. Com VPN, use o endereço do anfitrião no túnel. Em ambos os casos, o aplicativo acrescenta automaticamente a porta do jogo.

### WebRTC com STUN

1. O anfitrião escolhe **WebRTC (STUN)**, seleciona o deck, cria a sala e envia o convite gerado por mensagem privada.
2. O convidado cola o convite, gera a resposta e a devolve ao anfitrião.
3. O anfitrião cola a resposta e clica em **Conectar**.
4. Quando aparecer **Canal conectado**, o convidado seleciona o deck e entra. Os dois abrem o tabuleiro e mantêm os lobbies abertos durante a partida.

O STUN ajuda a descobrir endereços para a conexão direta. O DataChannel transporta os comandos e as atualizações. Algumas combinações de redes exigem um retransmissor TURN. O pacote WebRTC descrito usa STUN e troca manual de convite e resposta.

## 10. Instalação e distribuição

No Windows, execute o instalador `COGI Setup ... .exe` e abra o COGI pelo atalho. Para o multiplayer, os dois jogadores devem usar a mesma versão. O arquivo de deck pode ser criado no jogo ou enviado separadamente.

O modo contra a máquina utiliza o agente do COGI. Em uma sala multiplayer, os dois assentos são humanos. O servidor valida a prioridade e envia a cada jogador sua própria mão e as informações públicas do adversário. O anfitrião deve manter o aplicativo aberto para sustentar a partida.

**Escopo de validação:** o fluxo multiplayer em duas abas e a atualização das jogadas foram confirmados durante o desenvolvimento. A conexão WebRTC entre redes diferentes e a execução no instalador dependem da versão instalada e ainda precisam de validação de ponta a ponta.
