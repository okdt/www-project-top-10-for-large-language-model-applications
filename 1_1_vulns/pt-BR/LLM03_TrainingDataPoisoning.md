## LLM03: Envenenamento de Dados de Treinamento

### Descrição

O ponto de partida para qualquer abordagem de aprendizado de máquina é o conjunto de dados de treinamento, simplesmente "texto bruto". Para ser altamente capaz (por exemplo, ter conhecimento linguístico e mundial), esse texto deve abranger uma ampla variedade de domínios, gêneros e idiomas. Um modelo de linguagem grande (LLM) usa redes neurais profundas para gerar saídas com base em padrões aprendidos a partir dos dados de treinamento.

O envenenamento de dados de treinamento refere-se à manipulação dos dados de pré-treinamento ou dos dados envolvidos nos processos de ajuste fino ou incorporação para introduzir vulnerabilidades (que têm vetores de ataque únicos e, às vezes, compartilhados), backdoors ou viés que poderiam comprometer a segurança, eficácia ou comportamento ético do modelo. As informações envenenadas podem ser apresentadas aos usuários ou criar outros riscos, como degradação de desempenho, exploração de software downstream e danos à reputação. Mesmo que os usuários desconfiem da saída problemática da IA, os riscos permanecem, incluindo capacidades do modelo prejudicadas e possíveis danos à reputação da marca.

- Dados de pré-treinamento referem-se ao processo de treinar um modelo com base em uma tarefa ou conjunto de dados.
- O ajuste fino envolve pegar um modelo existente que já foi treinado e adaptá-lo a um assunto mais estreito ou a um objetivo mais focado, treinando-o com um conjunto de dados selecionado. Este conjunto de dados inclui normalmente exemplos de entradas e saídas desejadas correspondentes.
- O processo de incorporação é a conversão de dados categóricos (frequentemente texto) em uma representação numérica que pode ser usada para treinar um modelo de linguagem. O processo de incorporação envolve representar palavras ou frases dos dados de texto como vetores em um espaço vetorial contínuo. Os vetores são geralmente gerados alimentando os dados de texto em uma rede neural que foi treinada em um grande corpus de texto.

O envenenamento de dados é considerado um ataque à integridade porque interferir nos dados de treinamento afeta a capacidade do modelo de gerar previsões corretas. Naturalmente, fontes de dados externas apresentam maior risco, pois os criadores do modelo não têm controle sobre os dados ou um alto nível de confiança de que o conteúdo não contém viés, informações falsificadas ou conteúdo inadequado.


### Exemplos Comuns desta Vulnerabilidade

1. Um ator malicioso, ou uma marca concorrente, cria intencionalmente documentos imprecisos ou maliciosos direcionados aos dados de pré-treinamento, ajuste fino do modelo ou incorporação. Considere tanto [Envenenamento de Dados com Divisão de Visualização](https://github.com/GangGreenTemperTatum/speaking/blob/main/dc604/hacker-summer-camp-23/Ads%20_%20Poisoning%20Web%20Training%20Datasets%20_%20Flow%20Diagram%20-%20Exploit%201%20Split-View%20Data%20Poisoning.jpeg) quanto [Envenenamento de Dados com Antecipação](https://github.com/GangGreenTemperTatum/speaking/blob/main/dc604/hacker-summer-camp-23/Ads%20_%20Poisoning%20Web%20Training%20Datasets%20_%20Flow%20Diagram%20-%20Exploit%202%20Frontrunning%20Data%20Poisoning.jpeg) como vetores de ataque para ilustrações.
   1. O modelo vítima treina usando informações falsificadas, refletidas nas saídas de prompts de IA generativa para seus consumidores.
2. Um ator malicioso é capaz de realizar a injeção direta de conteúdo falsificado, tendencioso ou prejudicial nos processos de treinamento de um modelo, que é refletido nas saídas subsequentes.
3. Um usuário inadvertido está injetando indiretamente dados sensíveis ou proprietários nos processos de treinamento de um modelo, que são refletidos nas saídas subsequentes.
4. Um modelo é treinado com dados que não foram verificados por sua origem, conteúdo ou fonte em qualquer um dos exemplos de estágios de treinamento, o que pode levar a resultados errôneos se os dados estiverem contaminados ou incorretos.
5. O acesso irrestrito à infraestrutura ou a falta de isolamento adequado pode permitir que um modelo ingira dados de treinamento inseguros, resultando em saídas tendenciosas ou prejudiciais. Este exemplo também está presente em qualquer um dos exemplos de estágios de treinamento.
   1. Neste cenário, a entrada do usuário para o modelo pode ser refletida na saída para outro usuário (levando a uma violação), ou o usuário de um LLM pode receber saídas do modelo que são imprecisas, irrelevantes ou prejudiciais, dependendo do tipo de dados ingeridos em comparação com o caso de uso do modelo (geralmente refletido com um cartão de modelo).

*Seja um desenvolvedor, cliente ou consumidor geral do LLM, é importante entender as implicações de como essa vulnerabilidade pode refletir riscos em sua aplicação LLM ao interagir com um LLM não proprietário para entender a legitimidade das saídas do modelo com base em seus procedimentos de treinamento. Da mesma forma, os desenvolvedores do LLM podem estar em risco de ataques diretos e indiretos a dados internos ou de terceiros usados para ajuste fino e incorporação (mais comum), o que cria um risco para todos os seus consumidores.*

### Estratégias de Prevenção e Mitigação

1. Verifique a cadeia de suprimentos dos dados de treinamento, especialmente quando provenientes de fontes externas, e mantenha atestações por meio da metodologia "ML-BOM" (Machine Learning Bill of Materials), bem como verificação de cartões de modelo.
2. Verifique a legitimidade correta das fontes de dados direcionadas e dos dados obtidos durante os estágios de pré-treinamento, ajuste fino e incorporação.
3. Verifique o caso de uso para o LLM e a aplicação à qual se integrará. Crie modelos diferentes por meio de dados de treinamento
### Links de Referência

1. [Stanford Research Paper:CS324](https://stanford-cs324.github.io/winter2022/lectures/data/): **Stanford Research**
2. [How data poisoning attacks corrupt machine learning models](https://www.csoonline.com/article/3613932/how-data-poisoning-attacks-corrupt-machine-learning-models.html): **CSO Online**
3. [MITRE ATLAS (framework) Tay Poisoning](https://atlas.mitre.org/studies/AML.CS0009/): **MITRE ATLAS**
4. [PoisonGPT: How we hid a lobotomized LLM on Hugging Face to spread fake news](https://blog.mithrilsecurity.io/poisongpt-how-we-hid-a-lobotomized-llm-on-hugging-face-to-spread-fake-news/): **Mithril Security**
5. [Inject My PDF: Prompt Injection for your Resume](https://kai-greshake.de/posts/inject-my-pdf/): **Kai Greshake**
6. [Backdoor Attacks on Language Models](https://towardsdatascience.com/backdoor-attacks-on-language-models-can-we-trust-our-models-weights-73108f9dcb1f): **Towards Data Science**
7. [Poisoning Language Models During Instruction](https://arxiv.org/abs/2305.00944): **Arxiv White Paper**
8. [FedMLSecurity:arXiv:2306.04959](https://arxiv.org/abs/2306.04959): **Arxiv White Paper**
9. [The poisoning of ChatGPT](https://softwarecrisis.dev/letters/the-poisoning-of-chatgpt/): **Software Crisis Blog**
10. [Poisoning Web-Scale Training Datasets - Nicholas Carlini | Stanford MLSys #75](https://www.youtube.com/watch?v=h9jf1ikcGyk): **YouTube Video**
11. [OWASP CycloneDX v1.5](https://cyclonedx.org/capabilities/mlbom/): **OWASP CycloneDX**
