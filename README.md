
# Integração Unificada com Plataformas Sociais

Este repositório apresenta uma implementação em Java para unificar a interação com várias plataformas sociais — atualmente suportadas: Twitter, Instagram, LinkedIn e TikTok. O núcleo do projeto usa os padrões de projeto Adapter e Factory Method para encapsular peculiaridades de cada API e expor uma interface única ao restante da aplicação.

## Visão Geral do Design

O objetivo principal é isolar o código da aplicação das especificidades das APIs externas. Para isso:

- Cada serviço de rede social possui um adaptador que converte operações genéricas (por exemplo, publicar um post ou buscar métricas) em chamadas concretas da API dessa plataforma.
- Uma fábrica central (`SocialMediaFactory`) decide, em tempo de execução, qual adaptador criar com base no identificador da plataforma.

Com esse arranjo, adicionar suporte a uma nova rede exige implementar um novo adaptador e registrá-lo na fábrica — não há necessidade de alterar a lógica de publicação da aplicação.

## Padrões aplicados

- Adapter: padroniza as diferentes APIs para uma única interface (`SocialMediaAdapter`), permitindo que o restante do sistema trate todas as plataformas da mesma forma.
- Factory Method: centraliza a criação dos adaptadores dentro de `SocialMediaFactory`, promovendo coesão e reduzindo acoplamento.

## Fluxo de uso (modo de operação)

1. Crie uma instância de `Conteudo` com os dados da publicação (texto, mídia, etc.).
2. Solicite à `SocialMediaFactory` o adaptador correspondente à plataforma desejada.
3. Use o adaptador retornado para executar operações como publicar conteúdo ou recuperar `Estatisticas` da publicação.
4. Cada adaptador traduz essas chamadas para a API específica (autenticação, formato de payload, endpoints), garantindo uma experiência uniforme ao consumidor da API interna.

## Benefícios

- Extensibilidade: novas plataformas podem ser adicionadas com mudanças mínimas.
- Manutenibilidade: as diferenças entre APIs ficam confinadas aos adaptadores.
- Testabilidade: é possível mockar adaptadores para testes unitários sem depender das APIs reais.

---

Arquivo-chave:

- `adapter/SocialMediaAdapter.java` — interface comum dos adaptadores
- `factory/SocialMediaFactory.java` — responsável por instanciar adaptadores
- `model/Conteudo.java`, `model/Estatisticas.java` — modelo dos dados manipulados

Diagrama:

<img width="7125" height="1276" alt="diagrama" src="https://github.com/user-attachments/assets/392ce8b9-69d4-4107-bb1f-76be8f0914ab" />


