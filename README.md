# Treino City — servidor online (protótipo)

Este serviço mantém contas por nome, pedidos de amizade, convites, salas privadas, estado dos jogadores, vida/PvP e paredes sincronizadas. O site do jogo continua estático no Netlify; este servidor deve rodar separadamente e aceitar WebSockets.

## Publicar no Render

1. Envie a pasta `server` para um repositório GitHub.
2. No Render, crie **New → Web Service** e conecte o repositório.
3. Se o repositório contiver também o cliente, informe `server` como **Root Directory**. Se o repositório contiver somente os arquivos desta pasta, deixe o campo vazio.
4. Configure **Build Command** como `npm install` e **Start Command** como `npm start`.
5. O serviço usa a variável `PORT` fornecida pelo Render. Para conservar nomes e amizades entre reinícios, adicione um disco persistente montado em `/var/data` e defina `DATA_DIR=/var/data`. Sem armazenamento persistente, os perfis podem ser apagados quando a instância reiniciar ou for republicada.
6. Depois da publicação, copie o domínio `onrender.com`. No jogo, cada jogador informa `wss://SEU-DOMINIO.onrender.com/ws` no campo de servidor. A conexão segura é necessária para o site HTTPS.
7. Publique a pasta PWA do cliente no Netlify. Os dois jogadores precisam usar o mesmo endereço de servidor e a mesma versão do cliente.

## Regras desta versão de teste

- Até 8 jogadores por sala privada. O criador recebe um código de sala para compartilhar.
- Cadastro por nome único (3–16 letras, números ou `_`). O navegador gera uma chave de dispositivo e a guarda no armazenamento local; não há senha nem recuperação se os dados do navegador forem apagados.
- Pedidos de amizade podem ser aceitos ou recusados; amigos podem convidar para uma sala ativa.
- Há cinco paredes iniciais e cada jogador pode colocar até três paredes extras por sala.
- PvP é sincronizado pelo servidor, com vida, eliminação e reaparecimento. Os SGs continuam sendo inimigos locais controlados pelo jogo.
- É um protótipo: movimento vem do cliente e o servidor valida apenas faixa/ritmo básicos e distância do tiro; ainda não é anti-cheat de produção. Não use como sistema de contas seguro.
