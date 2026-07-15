# Notas de Análise do Conhecimento

> Análise arquitetural provisória sobre as questões apresentadas em [Estado Atual](estado-atual.md).
>
> Este documento formula hipóteses de trabalho. Não estabelece o modelo canônico nem substitui RFCs.

---

# Tese central

O Knowledge OS não deve tratar conhecimento como uma coleção de textos nem como uma resposta produzida por um modelo de IA.

Conhecimento é uma interpretação estruturada e revisável sobre algo, sustentada por evidências, situada em um domínio e relacionada a outras interpretações.

Documentos, conversas, código e observações são fontes ou manifestações. Eles não devem ser confundidos com o conhecimento que podem sustentar.

Portanto, a arquitetura deve separar com clareza:

- o que foi capturado;
- o que foi observado ou afirmado;
- a interpretação produzida;
- as evidências que a sustentam;
- as relações que lhe atribuem significado;
- o histórico de sua revisão.

Essa separação permite evolução sem apagar rastreabilidade e impede que uma fonte seja tomada, por si só, como verdade consolidada.

---

# Respostas provisórias

## Qual é a menor unidade de conhecimento?

A menor unidade não deve ser um documento, uma nota ou um fragmento textual.

Uma unidade mínima útil é uma **afirmação interpretável**: uma proposição que pode ser compreendida, relacionada, sustentada, contestada ou revisada.

Exemplos abstratos:

- "Captura e compreensão são atividades distintas."
- "A depende de B."
- "C é uma instância de D."

Essa unidade ainda não é necessariamente conhecimento consolidado. Ela pode estar em estado de hipótese, observação, afirmação ou princípio. O conhecimento emerge quando a afirmação recebe contexto, relações e sustentação suficientes para seu propósito.

## Como representar uma observação?

Uma observação deve registrar uma ocorrência percebida sem antecipar uma generalização.

Ela precisa, ao menos, de conteúdo, momento de registro, domínio ou contexto de uso e vínculo com a fonte que permitiu observá-la. Pode também registrar autor, método e limitações.

A observação preserva a evidência de partida. Uma interpretação posterior pode derivar dela, mas não deve alterar seu sentido original nem fazê-la passar por uma conclusão universal.

## Como distinguir informação de conhecimento?

Informação é um conteúdo registrado que reduz alguma incerteza em determinado contexto.

Conhecimento é informação interpretada, relacionada e suficientemente justificada para orientar compreensão ou ação.

Essa distinção não é binária nem definitiva. Uma mesma informação pode ser conhecimento operacional em um contexto e evidência insuficiente em outro. Por isso, o sistema deve representar grau de consolidação em vez de impor uma fronteira absoluta.

## Como representar autoridade, confiança e evidência?

Esses conceitos são diferentes e não devem ser reduzidos a uma única pontuação.

- **Evidência** é o que sustenta ou contesta uma afirmação.
- **Autoridade** é a competência, responsabilidade ou legitimidade de uma fonte em certo domínio.
- **Confiança** é a avaliação contextual de quanto uma afirmação pode orientar uma decisão.

Uma fonte pode ter alta autoridade e baixa evidência para uma afirmação específica. Muitas evidências podem existir sem que haja consenso sobre sua interpretação. A confiança deve ser derivada para um uso e momento determinados, mantendo explícitos seus fundamentos.

## Como modelar relações sem perder simplicidade?

O modelo inicial deve usar poucas relações semanticamente fortes, extensíveis apenas quando uma necessidade recorrente for demonstrada.

Um vocabulário inicial plausível inclui:

- sustenta / contesta;
- deriva de;
- depende de;
- relaciona-se com;
- é exemplo de;
- é parte de;
- substitui / revisa.

Cada relação deve declarar seus extremos, direção, significado e, quando necessário, evidência. Relações vagas demais tornam o grafo pouco interpretável; relações especializadas demais congelam prematuramente uma ontologia ainda em descoberta.

## Como permitir evolução contínua?

Evoluir não é sobrescrever o passado. É adicionar uma nova interpretação ou revisão, vinculada ao que a antecedeu.

O sistema deve preservar a proveniência das fontes e o histórico das afirmações, inclusive quando uma afirmação for corrigida, superada ou contestada. A visão atual pode privilegiar a interpretação mais bem sustentada, mas as versões anteriores devem continuar acessíveis.

## Como tornar o modelo independente de ferramentas?

O modelo canônico deve ser definido por conceitos, invariantes e relações, não por tabelas, APIs, formatos ou capacidades de um fornecedor.

Uma implementação pode usar Markdown, banco relacional, grafo, arquivos locais ou agentes de IA. Todas devem ser vistas como projeções do mesmo modelo conceitual. O teste de independência é simples: a semântica fundamental deve continuar válida se a tecnologia for substituída.

---

# Tensão arquitetural: generalização e proveniência

O princípio da generalização determina que o conhecimento consolidado não carregue contextos privados de sua descoberta.

Isso não elimina a necessidade de proveniência. A arquitetura deve distinguir dois níveis:

- a proveniência preserva, de modo controlado, que evidências sustentam uma afirmação;
- o conhecimento consolidado expressa apenas o padrão generalizável, sem depender de detalhes privados, acidentais ou pessoais.

Assim, uma experiência particular pode sustentar uma hipótese sem se tornar parte da formulação universal do princípio. O acesso à fonte e a exposição do princípio são responsabilidades diferentes.

---

# Hipótese de fluxo conceitual

Um fluxo mínimo coerente para a pesquisa atual é:

```text
Fonte -> Captura -> Observação -> Interpretação -> Afirmação
      -> Evidência e relações -> Revisão -> Conhecimento consolidado
```

O fluxo não é estritamente linear. Uma nova evidência pode contestar uma afirmação consolidada, e uma observação pode permanecer sem interpretação até que seu contexto seja compreendido.

---

# Implicações para as próximas RFCs

As duas RFCs já previstas devem estabelecer as fronteiras mais fundamentais:

1. **RFC-0001 — Observação**: definir observação, seus atributos mínimos, sua relação com fonte e a distinção entre registrar e interpretar.
2. **RFC-0002 — Captura vs. conhecimento**: definir os estágios do fluxo, critérios de transição e o que não pode ser considerado conhecimento consolidado.

Antes de uma ontologia ampla, convém criar RFCs para evidência e proveniência, ciclo de revisão e vocabulário inicial de relações. Essas decisões constituem o núcleo epistemológico do sistema; tecnologias e interfaces devem permanecer subordinadas a elas.
