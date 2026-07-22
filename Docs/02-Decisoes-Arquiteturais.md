# 02 - Decisões Arquiteturais

> **Documento anterior:** [01 - Arquitetura da Solução](01-Arquitetura.md)  
> **Próximo documento:** [03 - Fluxo Operacional](03-Fluxo-Operacional.md)

---

# Decisões Arquiteturais

## Objetivo

Toda arquitetura é resultado de decisões tomadas durante o desenvolvimento da solução.

Mais importante do que as tecnologias utilizadas é compreender os motivos que justificaram cada escolha.

Este documento apresenta os principais trade-offs considerados durante a definição da arquitetura do QA AI Orchestrator.

---

# Utilização do Microsoft Copilot Studio

O Microsoft Copilot Studio foi escolhido como camada conversacional da solução por oferecer um ambiente integrado ao ecossistema Microsoft, permitindo o desenvolvimento de agentes capazes de interpretar linguagem natural e interagir com diferentes serviços da plataforma.

Ao invés de atuar apenas como um chatbot, o agente foi projetado para conduzir o usuário durante o preenchimento das informações necessárias para o processo de homologação.

Sua responsabilidade está concentrada na interpretação, validação e estruturação dos dados informados durante a conversa.

## Benefícios

- Interface conversacional intuitiva.
- Integração nativa com Power Platform.
- Facilidade para evolução do agente.
- Menor complexidade de manutenção.
- Boa integração com fluxos automatizados.

## Trade-offs

| Vantagens | Limitações |
|-----------|------------|
| Desenvolvimento rápido | Dependência do ecossistema Microsoft |
| Integração nativa | Menor flexibilidade quando comparado a soluções totalmente customizadas |
| Baixa barreira de adoção | Personalizações avançadas dependem dos recursos da plataforma |

---

# Utilização do Excel como Repositório Operacional

Uma das principais decisões do projeto foi utilizar o Microsoft Excel como repositório operacional dos registros de homologação.

Essa escolha não foi motivada por limitações técnicas, mas pelo contexto operacional da solução.

Os usuários responsáveis pelas homologações já utilizavam planilhas como parte natural de suas atividades. Introduzir uma nova ferramenta exclusivamente para armazenamento das informações aumentaria a complexidade do processo e exigiria treinamento adicional.

Ao manter o Excel como fonte operacional, foi possível preservar o fluxo de trabalho já conhecido pelos usuários e reduzir a resistência à adoção da solução.

## Benefícios

- Ambiente familiar para os usuários.
- Baixa curva de aprendizado.
- Facilidade de manutenção.
- Simplicidade para consultas.
- Integração direta com Power Automate.

## Trade-offs

| Vantagens | Limitações |
|-----------|------------|
| Fácil utilização | Não substitui bancos de dados em cenários de alta escala |
| Fácil manutenção | Controle de concorrência limitado |
| Baixa complexidade operacional | Requer governança da estrutura da planilha |

---

# Utilização do Power Automate

A arquitetura separa claramente a inteligência conversacional da execução das automações.

Enquanto o agente é responsável pela interpretação das informações, o Power Automate atua exclusivamente na orquestração dos processos posteriores.

Essa separação reduz o acoplamento entre os componentes e facilita futuras evoluções da solução.

## Benefícios

- Centralização das integrações.
- Automação dos processos repetitivos.
- Facilidade para manutenção.
- Reutilização dos fluxos.
- Integração nativa com Microsoft 365.

## Trade-offs

| Vantagens | Limitações |
|-----------|------------|
| Plataforma Low-Code | Dependência da disponibilidade dos conectores |
| Fácil evolução | Fluxos muito complexos podem aumentar a manutenção |
| Integração nativa | Necessidade de governança dos fluxos |

---

# Utilização do Microsoft Word

A documentação de homologação normalmente exige registros formais que possam ser armazenados e compartilhados entre diferentes equipes.

Por esse motivo, a geração automática de documentos Word foi incorporada ao processo.

Ao utilizar modelos padronizados, a arquitetura reduz atividades repetitivas e aumenta a consistência das evidências produzidas durante os testes.

## Benefícios

- Padronização documental.
- Redução de retrabalho.
- Facilidade de compartilhamento.
- Compatibilidade com ambientes corporativos.

---

# Utilização do SharePoint

Os documentos produzidos durante a homologação precisam permanecer organizados e disponíveis para futuras consultas.

O SharePoint foi adotado como repositório documental por integrar-se naturalmente ao restante da arquitetura e oferecer um ambiente centralizado para armazenamento das evidências.

Sua responsabilidade limita-se ao gerenciamento dos documentos produzidos pelos processos automatizados.

---

# Utilização do Jira

O Jira foi definido como ferramenta de gerenciamento de incidentes da solução.

Sua utilização ocorre apenas quando o processo de homologação exige o registro de problemas identificados durante a execução dos testes.

Embora parte das informações possa ser preparada automaticamente, a classificação final permanece sob responsabilidade do usuário.

Essa decisão preserva o julgamento humano em situações que dependem do conhecimento do contexto operacional.

---

# Por que a IA não toma decisões sobre regras de negócio?

Um dos princípios adotados durante o desenvolvimento da solução foi limitar a atuação da Inteligência Artificial às atividades relacionadas à organização das informações.

Ambientes corporativos frequentemente apresentam regras altamente customizadas, tornando inviável que um agente interprete corretamente todos os cenários apenas com conhecimento genérico.

Nesse contexto, o papel da IA é apoiar o usuário durante o processo de documentação, e não substituir sua experiência sobre o sistema homologado.

Essa abordagem reduz o risco de interpretações incorretas e mantém a responsabilidade pelas decisões de negócio com os especialistas responsáveis pelo processo.

---

# Por que o usuário continua responsável por determinadas informações?

Determinadas informações exigem análise contextual e conhecimento específico sobre o ambiente de homologação.

A classificação de incidentes, priorização de problemas e validação do comportamento esperado permanecem sob responsabilidade do usuário, pois dependem de critérios que variam conforme o processo de negócio.

A arquitetura foi projetada para automatizar atividades operacionais sem eliminar a necessidade de validação humana nos pontos críticos do processo.

---

# Papel da Inteligência Artificial na Arquitetura

A Inteligência Artificial atua como uma camada de apoio operacional.

Sua principal responsabilidade consiste em transformar informações desestruturadas em registros padronizados, garantindo maior qualidade para as etapas posteriores do processo.

A solução não foi concebida para substituir especialistas de negócio.

Seu objetivo é reduzir esforço operacional, aumentar consistência documental e melhorar a qualidade das informações produzidas durante as homologações.

---

# Resumo das Decisões

| Decisão | Objetivo |
|---------|----------|
| Microsoft Copilot Studio | Estruturar informações através de IA Conversacional |
| Excel | Centralizar os registros operacionais |
| Power Automate | Orquestrar integrações e automações |
| Word | Gerar evidências padronizadas |
| SharePoint | Armazenar documentos produzidos |
| Jira | Gerenciar incidentes identificados durante os testes |
| Usuário | Permanecer responsável pelas decisões relacionadas ao negócio |

---

# Considerações Finais

As decisões apresentadas neste documento foram orientadas pelo contexto do problema e pelas características do ambiente operacional.

Ao priorizar ferramentas já adotadas pelos usuários e distribuir responsabilidades entre componentes especializados, a arquitetura busca equilibrar simplicidade de utilização, padronização dos processos e facilidade de manutenção.

---

⬅️ **Documento anterior:** [01 - Arquitetura da Solução](01-Arquitetura.md)

➡️ **Próximo documento:** [03 - Fluxo Operacional](03-Fluxo-Operacional.md)