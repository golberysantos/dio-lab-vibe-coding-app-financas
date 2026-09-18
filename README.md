# 💸 App de Organização de Finanças Pessoais com Vibe Coding

Aplicativo de organização de finanças pessoais que funcione por meio de conversas em linguagem natural.  
O objetivo é tornar o controle financeiro mais intuitivo, acessível e livre de burocracias como planilhas ou formulários complexos.
Aplicativo criado com uso de ferramentas como o **Copilot** e o **Lovable** com uma comunicação simples e natural para, acima de tudo, aprender o **jeito Vibe de programar com IA**.

> [!IMPORTANT]
> O foco está em **usar a IA como parceira criativa**, transformando boas ideias e prompts em conceitos funcionais que simulam um produto real.

## ✨ O que é Vibe Coding

**Vibe Coding** é uma forma leve e criativa de desenvolver com IA, baseada em **conversas naturais e bem estruturadas**. Em vez de escrever código linha por linha, **guia-se a IA** descrevendo suas ideias de forma clara, com **intenção e contexto** para criar o código. Em outras palavras:

> Você mostra a vibe da sua ideia e a IA transforma em solução (ou em um caminho para ela).

--- 

## 🎯 Desafio

Problema: Muitas pessoas não conseguem manter um controle financeiro porque os aplicativos exigem muita entrada de dados manual, e a criação de orçamentos é vista como algo tedioso. 

---
## Funcionalidades 

Segue as funcionalidades criadas por outros desenvolvedores e as minhas funcionalidades contribuitivas.  

### 🔍 Funcionalidades Criadas (Base - Template conversa-fin-amigo.lovable.app)
1. **Dashboard Financeiro**
    - Receitas: Total de ganhos registrados
    - Despesas: Total de gastos
    - Saldo: Diferença entre receitas e despesas
    - Interface simples e direta para facilitar a compreensão

2. **Assistente Financeiro**
    - Personagem conversacional que interage com o usuário
    - Incentiva a conexão de contas e cartões para uma visão completa das finanças
    - Oferece suporte emocional e motivacional

3. **Registro de Transações via Chat**
    - Campo de entrada para o usuário digitar mensagens em linguagem natural
    - Permite registrar gastos e interagir com o assistente de forma fluida

4. **Metas Financeiras**
    - Área dedicada à criação e acompanhamento de objetivos financeiros
    - Sugestão proativa para o usuário definir metas
    - Botão de ação para adicionar novas metas

5. **Relatórios Personalizados**
    - Visualizações simples e adaptadas ao estilo do usuário
    - Acompanhamento de metas e progresso financeiro

6. **Design Universal**
    - Interface acessível e inclusiva:
        - Linguagem simples
        - Navegação clara
        - Compatibilidade com leitores de tela e comandos por voz
        - Feedbacks visuais e auditivos para facilitar o uso

### 🚀 Minhas funcionalidades - Contribuição Autoral (Golbery Santos)

#### 7. Cofrinhos Inteligentes (Smart Pockets) - Bounded Context `Savings`
**Problema que resolve:** Metas financeiras abstratas ("economizar R$500") não geram engajamento. Usuários abandonam.

**Solução:** Evolução do conceito de Metas para **Envelopes Visuais Gamificados**.

**Implementação Técnica:**
- **DDD:** Novo Aggregate Root `Cofrinho` com Value Objects `Dinheiro` e `Progresso`. Invariante: `atual <= meta`. Desacoplado de `Transaction` para evitar Big Ball of Mud.
- **Arquitetura:** Hook `useCofrinhos.ts` com persistência em `localStorage (smart_pockets_v1)`. Componentes desacoplados: `CofrinhoCard.tsx`, `NovoCofrinhoDialog.tsx`, `CofrinhosEmpty.tsx`.
- **Design System Fiel:** Extraí a paleta da referência (print `Minha Carteira`): Background `#F8FBF9`, Cards `bg-white rounded-xl border-slate-200`, Primary `#22C55E` (botão Nova Meta), Despesa `#EF4444`. Trava obrigatória de `shadcn/ui` (Card, Button, Progress, Dialog) para manter consistência visual e WCAG AA.
- **Integração com Chat Natural (Vibe Coding):** Nova intenção `ALLOCATE_SAVING` no parser. Regex `/ (guardei|guardar)\s*R?\$?\s*(\d+)\s*para\s*([a-z]+)/i` permite "guardei R$50 para viagem" → aloca no cofrinho correspondente + toast animado + Progress anima.
- **Gamificação:** Desafio 52 semanas opcional dentro de cada cofrinho, com timeline de aportes crescentes.
- **Stack:** React + TypeScript + Tailwind + shadcn/ui, lucide-react, sem libs extras.

**Link do meu projeto no Lovable:** [seu-projeto-pessoal.lovable.app] (substituir após criar)

---

## 🧠 Reflexão

### O que funcionou bem?
1. **Travar Design System no prompt:** Ao extrair os hex exatos da print (#F8FBF9, #22C55E) e obrigar o uso de `shadcn/ui` (`@/components/ui/card`, `button`, `progress`), o Lovable gerou a feature 100% consistente com o template original em apenas 1 interação, sem inventar cores ou divs custom.
2. **Abordagem por Bounded Context:** Criar um contexto `Savings` separado de `Transactions` evitou acoplar lógica no Dashboard e preveniu o anti-pattern God Component. Facilitou testes e manutenção.
3. **Vibe Coding Estruturado:** Usar formato Contexto > Design System > Regras Técnicas > User Flow > Critérios de Aceite fez a IA entender intenção e não só UI.
4. **Integração Chat + Domínio:** A intenção `ALLOCATE_SAVING` mostrou o poder da linguagem natural - o usuário não precisa sair do chat para guardar dinheiro, mantendo o princípio do PRD de "livre de burocracias".

### O que não funcionou como o esperado?
1. **Acesso ao template base:** Tentei editar diretamente `conversa-fin-amigo.lovable.app`, mas é apenas uma vitrine pública (read-only). É política de segurança do Lovable (LIVE_CRAWL_POLICY_BLOCKED). Tive que recriar o MVP base no meu Lovable pessoal usando a print como Style Reference.
2. **Parser de linguagem natural inicial:** Na primeira iteração, o Lovable entendeu "guarde R$50 para viagem" como despesa e não como alocação. Tive que refinar o regex e adicionar exemplos few-shot no prompt ("Ex: 'guardei 20 para casa' → alocação").
3. **Cor do Progress:** O componente `Progress` do shadcn vem com `bg-primary` padrão. Tive que forçar `indicatorClassName="bg-[#22C55E]"` para manter a consistência com o botão "Nova Meta", senão ficava com tonalidade diferente.
4. **Créditos do Lovable:** Como relatado por outros devs, os créditos gratuitos acabam em 3 interações. Por isso, dividir em 2 prompts bem estruturados (1 base + 1 feature) foi crucial.

### O que aprendi sobre conversar com IAs?
Aprendi que Vibe Coding não é "prompt solto e torcer". É **arquitetura por prompt**:
- **Restrição gera criatividade:** Quanto mais restritivo (use apenas shadcn, use apenas #22C55E, não crie divs custom), mais consistente e profissional a IA entrega dentro do Design System.
- **Falar como Tech Lead:** Definir Bounded Context, contratos TypeScript (`type Cofrinho`), storage key e critérios de aceite evita que a IA gere código anêmico ou Big Ball of Mud.
- **Imagem como prompt:** Anexar a print de referência vale mais que 100 linhas descrevendo cor. O Lovable entende visualmente o `rounded-xl`, `border-slate-200` e `shadow-sm`.
- **Iteração é design:** O primeiro output nunca é o final. É preciso testar a usabilidade (ex: digitar "guardei R$30") e voltar com feedback cirúrgico, igual faria com um dev junior.

## 🔗 Links
- Template base de referência: https://conversa-fin-amigo.lovable.app
- Meu projeto com a nova feature: https://minty-my-wallet.lovable.app
- Protótipo no Figma (se criar): [link]

## 🛠️ Como rodar local (se exportar do Lovable)
```bash
npm install
npm run dev
```
