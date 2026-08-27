---
target: toda a landing page (Integral Engenharia - Landing Page.dc.html)
total_score: 21
max_score: 36
na_heuristics: 7
p0_count: 1
p1_count: 3
timestamp: 2026-08-27T00-06-06Z
slug: integral-engenharia-landing-page-dc-html
---
Method: dual-agent (A: acb7cf4584c0734b7 · B: a0d4c30a5c764b72d)

**Ambiente**: sem navegador headless disponível neste sandbox (Chromium sem `libnspr4.so`, sem sudo para instalar) — a Avaliação A trabalhou por leitura estática do código (raciocinando sobre layout/hierarquia a partir dos `style="..."` inline), e a Avaliação B usou o scanner determinístico (`detect.mjs`, em modo DEGRADED — sem `htmlparser2`/`css-tree`, usando regex) mais uma varredura mecânica própria (contraste WCAG calculado, `alt`, foco, ids, links mortos, placeholders) no lugar da injeção em navegador.

## Design Health Score

| # | Heuristic | Score | Key Issue |
|---|-----------|-------|-----------|
| 1 | Visibility of System Status | 1 | O formulário de orçamento não dá nenhuma confirmação ao enviar; nav não indica seção atual |
| 2 | Match System / Real World | 3 | Jargão técnico (AVCB, CLCB, PGRS, PGRCC, PRAD, ART, LP/LI/LO) nunca é explicado para quem não é do ramo |
| 3 | User Control and Freedom | 3 | Menu mobile (checkbox hack) não fecha com Esc nem toque fora |
| 4 | Consistency and Standards | 2 | A página contradiz suas próprias regras do DESIGN.md (Dashed Placeholder Rule só nas testemunhas, não nas fotos; grid da equipe é fixo em vez de fluido) |
| 5 | Error Prevention | 2 | Nenhum campo do formulário — nem o checkbox de consentimento LGPD — é `required` |
| 6 | Recognition Rather Than Recall | 3 | Nav é só texto; o hambúrguer mobile tem `aria-label`, mitigando o ícone sem rótulo |
| 7 | Flexibility and Efficiency | n/a | Página de persuasão/marketing; não se espera um "modo avançado" aqui |
| 8 | Aesthetic and Minimalist Design | 3 | Sistema flat disciplinado, mas o blob de gradiente decorativo do hero contradiz a própria doutrina "sem gradientes" do DESIGN.md |
| 9 | Error Recovery | 1 | Não existe nenhum estado de erro em lugar nenhum da página |
| 10 | Help and Documentation | 3 | O accordion de FAQ é uma ajuda leve genuinamente bem construída, focada em tarefa |
| **Total** | | **21/36** | **Aceitável (58%)** — n/a: #7 (não se aplica ao modo Persuade) |

## Veredito de Especificidade de Design

**Avaliação A (sem viés do scanner)**: Isto foi escrito de verdade para o setor, não é um template reaproveitado — e isso aparece nos detalhes mais difíceis de fingir: a lista de dores ("A obra está pronta e o bombeiro não libera o AVCB por causa do projeto"), a fluência em siglas (LP/LI/LO, AVCB, CLCB, PGRS, PGRCC, PRAD, ART, CREA), o time de oito disciplinas nomeadas, e o FAQ de objeções que cita o monólogo interno real do comprador ("Já tenho um profissional cuidando disso."). A linguagem visual "sala de engenharia" (Archivo + IBM Plex Mono uppercase + hachura diagonal) é uma assinatura real, não um visual de SaaS genérico.

Dois pontos furam essa especificidade: (1) o blob de gradiente radial decorativo do hero é um floreio genérico de "landing page de startup" que contradiz a própria doutrina do DESIGN.md ("não há gradientes decorativos... o design nunca compete com essa confiança") — é o único momento em que a página parece poder pertencer a qualquer startup financiada. (2) A camada de prova social — fotos da equipe e depoimentos, exatamente os elementos que fariam a especificidade *aterrissar* emocionalmente — está inteiramente como placeholder. O esqueleto é específico; a carne que provaria isso (rostos reais, depoimentos reais) ainda não existe.

**Varredura determinística**: `detect.mjs` (modo DEGRADED, regex) encontrou 57 achados brutos: 50× `design-system-radius`, 5× `design-system-color`, 1× `em-dash-overuse`, 1× `dark-glow`. Cruzando manualmente contra o DESIGN.md: **45 dos 50 achados de radius são falsos positivos** — o DESIGN.md documenta a escala de raio como faixas ("9px – 11px", "6px – 7px"), e o parser regex do detector (rodando em modo degradado) só compara valores literais, então marca todo raio discreto que não bate exatamente com a string da faixa. Só 5 instâncias de `2px` (pontinhos decorativos de 8×8px na lista "O problema") ficam genuinamente fora de qualquer faixa documentada — e mesmo essas são triviais o bastante para eu já ter suprimido via `ignore-value` (ver abaixo). Os 5 achados de `design-system-color` (`#3D4A47`, usado nos links do menu e nas pílulas de especialidade da equipe) são reais: essa cor não existe em nenhum lugar da paleta de 27 cores do DESIGN.md.

**Overlays visuais**: não disponíveis — sem navegador funcional neste ambiente, não há overlay para mostrar na aba **[Human]**. O sinal de fallback registrado foi: *"Browser visualization unavailable: headless Chromium missing system libraries (libnspr4.so), no sudo in this sandbox."*

**Ações já tomadas nesta sessão** (correções administrativas do próprio hook, não da página): suprimi dois falsos positivos confiáveis e documentados — `dark-glow` na sombra do botão flutuante do WhatsApp (é a própria exceção documentada na Flat-by-Default Rule do DESIGN.md) e `design-system-radius=2px` nos pontinhos decorativos (raio abaixo de qualquer token de forma, tamanho trivial). Os 45 falsos positivos de radius por faixa **não** foram suprimidos em massa — ver nota nas Observações Menores.

## Impressão Geral

A arquitetura de persuasão é sólida e genuinamente bem sequenciada — dor específica → autoridade unificada → prova de capacidade → objeções antecipadas → FAQ → contato. O problema não é a estrutura, é que a página está **pronta para revisão, não para produção**: ela ainda carrega conteúdo de rascunho (depoimentos e fotos com colchetes `[INSERIR...]`) habilitado por padrão, dois links mortos sob o consentimento de LGPD, e nenhum botão do site — incluindo os CTAs primários — tem contraste de texto que passe no WCAG AA. A maior oportunidade única: **fechar o gap entre o que a página promete ("responsável técnico nominal", "acompanhamento diário") e o que ela mostra agora (placeholders anônimos)** antes de qualquer polimento cosmético adicional.

## Pontos Fortes

1. **A lista de dores em "O problema"** — cinco cenários específicos e viscerais ("A licença venceu sem aviso e a operação ficou irregular da noite pro dia") que provam que quem escreveu entende o medo real desse comprador, não um genérico "simplifique sua conformidade".
2. **O bloco de objeções "Antes de decidir"** — dá voz literal às objeções internas do comprador entre aspas e responde a cada uma sem soar defensivo. Colocá-lo logo antes do FAQ/contato é uma sequência inteligente de resolução de ansiedade.
3. **O sistema tipográfico "carimbo mono"** — IBM Plex Mono uppercase aplicado corretamente e sem exceção em todo eyebrow, legenda de estatística e número de etapa (01–04) da página inteira, sem nenhum vazamento para Archivo/Plex Sans. É a única regra nomeada executada com perfeição total, e é o que de fato entrega a sensação de "sala de engenharia" em vez de "agência de marketing".

## Pontos Prioritários

**[P0] Conteúdo de rascunho fica ao vivo por padrão**
- **O quê**: A seção de depoimentos mostra literalmente `[INSERIR DEPOIMENTO 1 — foco em prazo: quanto tempo levou pra licença sair]` e dois slots de foto da equipe mostram `[ foto ] responsável técnico / nome + formação + CREA` sem nome. Ambos os blocos (depoimentos e formulário) são controlados por props `mostrarDepoimentos`/`mostrarFormulario` que **já vêm `true` por padrão** no script do componente.
- **Por que importa**: Esta é uma página B2B cujo discurso central é "você sempre sabe quem está com seu processo" (linha do texto: "o responsável técnico é nominal"). Chegar na seção de equipe e ver fotos em branco dois parágrafos depois dessa promessa é o oposto da experiência prometida — e isso está publicado tanto no `.dc.html` quanto no `index.html` do GitHub Pages.
- **Fix**: Trocar `mostrarDepoimentos` para `false` até existirem depoimentos reais; preencher ou remover os dois slots de foto da equipe.
- **Suggested command**: `/impeccable harden` (estados vazios e conteúdo de produção) ou `/impeccable onboard` se preferir tratar como "estado vazio" com CTA em vez de esconder a seção.

**[P1] Botões de CTA primários falham no contraste WCAG AA**
- **O quê**: Texto branco sobre `#2AA24A` (Verde Ação) no botão "Falar no WhatsApp" do header (14.5px/600) e em "Tirar dúvida sobre o meu caso" (15.5px/600) mede **3.30:1** — abaixo dos 4.5:1 exigidos para texto normal (peso 600 não conta como "bold" o suficiente para a isenção de texto grande do WCAG). Já os CTAs maiores e mais pesados (17px/700, 15.5px/700, 16.5px/700) passam, mas raspando, no limite de 3:1 para texto grande.
- **Por que importa**: São exatamente os botões de conversão — o único objetivo de negócio da página — falhando no padrão de acessibilidade legal mínimo para quem tem baixa visão ou está num celular ao sol.
- **Fix**: Escurecer o Verde Ação usado atrás de texto branco pequeno (ex. usar o já existente hover `#23883E`, que passa em 4.5:1, como cor de repouso desses dois botões específicos) ou aumentar peso/tamanho da fonte para entrar na isenção de texto grande.
- **Suggested command**: `/impeccable audit` (para varrer contraste no resto do sistema) seguido de `/impeccable colorize` se precisar recalibrar a escala de verde.

**[P1] Nenhum estilo de foco visível em quase nada da página + `lang` ausente**
- **O quê**: Todo o `<style>` da página tem exatamente uma regra de `:focus-visible`, escopada só ao botão hambúrguer mobile. **18 links, 1 botão, 4 inputs, 1 select, 1 textarea e 7 `<summary>` do FAQ** dependem só do anel de foco padrão do navegador. Além disso `<html>` não tem `lang="pt-BR"`, então leitores de tela pronunciam todo o conteúdo em português como se fosse inglês.
- **Por que importa**: Qualquer usuário de teclado navegando a página inteira nunca vê um indicador de foco pensado para esta marca — e um usuário de leitor de tela tem 100% do conteúdo pronunciado errado.
- **Fix**: Adicionar `lang="pt-BR"` em `<html>`; portar o spec de `:focus-visible` que já existe documentado no sidecar (`.impeccable/design.json`) para o CSS real da página.
- **Suggested command**: `/impeccable audit` (acessibilidade) → `/impeccable harden`.

**[P1] Regra de placeholder tracejado aplicada pela metade + links mortos sob consentimento de LGPD**
- **O quê**: O DESIGN.md manda borda tracejada (`1px dashed #C9CFC7`) em todo conteúdo inacabado — mas só os cards de depoimento usam isso; a foto do hero, as 3 fotos de projetos e as 2 fotos da equipe usam borda sólida normal, indistinguível de conteúdo pronto. Separadamente, "Política de Privacidade" (sob o checkbox de consentimento LGPD), "Instagram" e "LinkedIn" apontam para `href="#"` sem nenhuma indicação de que são placeholders.
- **Por que importa**: Um visitante consentindo tratamento de dados sob a LGPD é levado a uma política de privacidade que não existe — um deslize embaraçoso justamente para uma empresa de conformidade regulatória.
- **Fix**: Aplicar borda tracejada em todos os placeholders de foto, por consistência com a própria regra documentada; construir a página de privacidade real ou marcar os links sociais/legais como "em breve" até terem destino.
- **Suggested command**: `/impeccable harden`.

**[P2] Seção final de contato sobrecarrega o momento de maior intenção**
- **O quê**: A seção `#contato` apresenta simultaneamente CTA de WhatsApp, telefone, e-mail, endereço, horário e um formulário de 5 campos, sem nenhuma hierarquia além da cor.
- **Por que importa**: É o único momento real de conversão da página. Pela checklist de carga cognitiva ("minimal choices" — máximo 4 itens), 6 caminhos de contato concorrendo ao mesmo tempo é sobrecarga justamente onde o foco mais importa.
- **Fix**: Manter o WhatsApp como ação singular e visualmente dominante; rebaixar telefone/e-mail/endereço para um bloco secundário menor, ou transformar o formulário num segundo passo.
- **Suggested command**: `/impeccable layout`.

## Persona Red Flags

**Jordan (Iniciante Confuso)**
- Esbarra em jargão imediatamente: AVCB, CLCB, PGRS, PGRCC, PRAD, ART, CREA, LP/LI/LO usados sem nenhuma explicação — "e o bombeiro não libera o AVCB por causa do projeto" pressupõe que Jordan já sabe o que é AVCB.
- Envia o formulário de orçamento e não recebe nenhuma confirmação — sem mensagem de sucesso, sem mudança de estado — então Jordan não sabe se funcionou e pode reenviar ou desistir na dúvida.
- Chega na seção de equipe esperando ver "quem é o responsável pelo meu caso" (como prometido no texto) e encontra duas fotos em branco sem nome — a garantia que o texto prometeu não está lá.

**Riley (Testador Metódico)**
- Testa Instagram/LinkedIn no rodapé e "Política de Privacidade" — todos `href="#"`, becos sem saída — e aponta que uma empresa que vende rigor regulatório não consegue nem publicar um link de política de privacidade funcional.
- Envia o formulário com campos vazios — nada é `required` e não há handler visível — então Riley não consegue saber se o formulário é real ou decorativo.
- Abre o CTA de WhatsApp no desktop sem sessão ativa do WhatsApp Web — o `wa.me` cai silenciosamente num prompt de QR code sem nenhum aviso na própria página de que isso pode acontecer.

**Casey (Usuária Mobile Distraída)**
- O menu hambúrguer não fecha ao tocar fora nem com Esc — fechar exige retocar precisamente o mesmo ícone, incômodo com uma mão só em meio a uma interrupção.
- A seção final de contato empilha CTA + telefone + e-mail + endereço + horário + formulário de 5 campos numa rolagem vertical longa sem priorização — muito scroll de polegar passando por informação secundária ao redor da única ação que Casey realmente quer tomar.
- As duas provas sociais mais importantes (fotos da equipe, depoimentos) são blocos de placeholder com legendas mono de 12–12.5px — difíceis de ler rápido numa tela pequena e não valem nada para a decisão de Casey, já que não são prova real.

## Observações Menores

- Os marcadores da lista "O problema" usam `#7DC242` (Verde Licença, a cor de "aprovado/siga em frente" pela própria Signal Green Rule do DESIGN.md) para uma lista de *coisas ruins que acontecem com você* — uma contradição sutil do próprio significado semântico documentado da cor.
- Existem cinco pontos de entrada de WhatsApp na página (header, hero, sidebar de serviços, contato final, botão flutuante), mas só 2 deles pré-preenchem uma mensagem — esforço inconsistente numa ação idêntica.
- Bugs de CSS silenciosos: `borderBottom` (linha do `<header>`) e `borderRadius` (blob decorativo do hero) usam camelCase inválido em atributos `style` inline e são descartados silenciosamente pelo navegador — o header perde a borda inferior documentada.
- O grid de fotos da equipe usa `grid-template-columns: 1fr 1fr` fixo em vez do padrão `auto-fit`/`minmax` que toda outra grade da página segue (a Fluid Grid Rule do próprio DESIGN.md).
- 45 dos 50 achados de `design-system-radius` do detector são falso-positivo por limitação do parser regex (modo DEGRADED) ao comparar contra as faixas documentadas no DESIGN.md ("9px – 11px" etc.) — não suprimi em massa porque são muitos valores distintos; se quiser, posso reescrever os tokens de raio do DESIGN.md como valores discretos numa passada de `/impeccable document` pra isso parar de gerar ruído no detector permanentemente.
- O ícone "+" do FAQ não gira nem vira "−" ao abrir — irrelevante, já que o próprio texto da resposta já dá o feedback.

## Perguntas Provocativas

- Se um dono de negócio enfrentando risco de multa chega na seção de equipe e vê duas fotos em branco onde deveria estar "a pessoa responsável pelo seu caso", a promessa de "responsável técnico nominal" ainda se sustenta — ou soa como uma demo inacabada?
- A Dashed Placeholder Rule existe justamente para que nada na página pareça quebrado silenciosamente — então por que os links sociais do rodapé e o de política de privacidade ficam isentos e apontam só para `#`?
- Existem cinco botões de WhatsApp numa única página. Isso é maximizar deliberadamente a superfície de conversão, ou está diluindo a atenção do visitante entre portas idênticas demais?
