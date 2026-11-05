# 🐭 Toca Limpa - Gestão da Casa & Micro-Tarefas com o Remi

Aplicativo web completo, responsivo e com arquitetura PWA (Progressive Web App) para organização e gestão de micro-tarefas da casa a dois, com sincronização em tempo real via **Firebase Firestore**, gamificação com o mascote **Remi** (um ratinho twister cinza chumbo) e espaço privado individual.

![Toca Limpa Preview](IMG-20241121-WA0011.jpeg)

---

## ✨ Funcionalidades

### 1. 🐭 Mascote Dinâmico (Remi) & Progresso Semanal
- O mascote do app foi ilustrado e inspirado fielmente no ratinho twister **Remi** (pelagem cinza chumbo, orelhas grandes rosadas, patinhas com luvas brancas e olhinhos atentos).
- A barra de progresso no topo da aba compartilhada reage dinamicamente às tarefas concluídas na semana:
  - **0% a 24%:** Remi dormindo enroladinho na caminha com partículas de `Zzz...`
  - **25% a 49%:** Remi curioso com as orelhinhas em pé: *"Bora arrumar a toca?"*
  - **50% a 74%:** Remi feliz sentado roendo um petisco (semente crocante) com as bochechas cheias.
  - **75% a 99%:** Remi festejando e dando pulinhos de alegria.
  - **100%:** Remi coroado com coroa de ouro, troféu de vitória e chuva comemorativa de confetes (`canvas-confetti`)!

### 2. 🎨 Perfis com Identidade Visual Dinâmica
- Seletor rápido na barra superior para alternar com 1 toque entre os moradores (**Ana** e **João**).
- Cada morador pode escolher sua cor tema (Lilás/Roxo, Rosa, Verde, Azul, Amarelo, Coral).
- Toda a interface (bordas de cards, botões ativos, barra de progresso, tags e destaques) se adapta instantaneamente à cor do usuário ativo.

### 3. 🗓️ Ciclo Semanal com Reset Automático Inteligente
- As tarefas compartilhadas da casa ficam gravadas na coleção `household_tasks`.
- O app calcula o ciclo da semana atual (`week-YYYY-MM-DD` com início no domingo à meia-noite).
- Quando a semana vira (domingo às 00:00), todas as tarefas da casa voltam automaticamente para o estado pendente, preservando a lista base de tarefas cadastradas sem necessidade de servidores ou cron jobs externos!
- Ao marcar uma tarefa, ela exibe o carimbo com o nome e a cor de quem fez (ex: *"✓ Feito por Ana"*).
- Botões de filtro rápido no topo:
  - **Todas:** Exibe todas as tarefas da casa.
  - **Minhas:** Filtra as tarefas concluídas pelo usuário ativo na semana.
  - **De [Outro]:** Filtra as tarefas concluídas pelo parceiro.

### 4. 🔒 Espaço Estritamente Privado ("Só para Mim")
- Aba individual com isolamento de dados real:
  - No Firestore: gravado em subcoleções exclusivas `user_private_spaces/{profileId}/tasks`.
  - No modo local: gravado sob chaves isoladas `toca_private_tasks_{profileId}`.
- O morador parceiro **não** tem acesso, não lista e não recebe atualizações das tarefas privadas do outro.

---

## 🛠️ Tecnologias Utilizadas
- **React 18** (via CDN)
- **Tailwind CSS v3** (Play CDN com suporte a CSS Variables dinâmicas)
- **Firebase Firestore v9 Compat** (Sincronização em tempo real & Fallback LocalStorage)
- **Canvas Confetti** (Efeitos de celebração ao bater 100%)
- **Babel Standalone**

---

## 🚀 Como Executar

Basta abrir o arquivo `index.html` diretamente em qualquer navegador moderno (Google Chrome, Microsoft Edge, Safari, Firefox).

Para usar no celular como um app nativo (PWA):
1. Abra a página no navegador do celular.
2. Toque no menu de opções do navegador e selecione **"Adicionar à Tela de Início"**.

---

## ⚙️ Configuração do Firebase (Opcional)

Por padrão, o app já funciona 100% no **Modo Local (LocalStorage)**. Para habilitar a sincronização em tempo real entre celulares e computadores:

1. Acesse o [Firebase Console](https://console.firebase.google.com/) e crie um projeto gratuito.
2. Ative o **Cloud Firestore Database** (em modo de teste para uso familiar).
3. Abra o arquivo `index.html` e cole suas credenciais no objeto `firebaseConfig`:

```javascript
const firebaseConfig = {
  apiKey: "SUA_API_KEY",
  authDomain: "SEU_PROJETO.firebaseapp.com",
  projectId: "SEU_PROJECT_ID",
  storageBucket: "SEU_PROJETO.appspot.com",
  messagingSenderId: "SEU_MESSAGING_SENDER_ID",
  appId: "SEU_APP_ID"
};
```
