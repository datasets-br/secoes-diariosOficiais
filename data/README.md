*Datasets* descritores (metadados) dos diários oficiais do Brasil.

Maiores detalhes: compor [`datapackage.json`](../datapackage.json) na raiz, em conformidade com [specs.frictionlessdata.io](http://specs.frictionlessdata.io/) ou [exemplo](https://github.com/datasets-br/state-codes/blob/master/datapackage.json).

Para editar os dados, preferir o uso  [desta planilha colaborativa](https://docs.google.com/spreadsheets/d/1w9oLo9ejbOuweLrss_FddZ-ZiqYZaNJmapUF_Rk28nU/), depois de revisado faz download para cá.

## URN LEX como referência

A organização dos *metadados de controle* para recuperação de dados relativos a Diários Oficiais 
têm como base a definição da [URN-LEX](https://en.wikipedia.org/wiki/Lex_(URN)) na [RFC-draft-urn-lex-v10](https://datatracker.ietf.org/doc/draft-spinosa-urn-lex/),
já adotada no Brasil desde 2009 com o início das operações do Portal LexML e da vigência da norma [LexML-URN](http://projeto.lexml.gov.br/documentacao/Parte-2-LexML-URN.pdf), reforçada pelo [E-PING](http://eping.governoeletronico.gov.br/#p2s5) desde 2010.

No cenário internacional o uso de *identificadores transparentes* similares à  URN LEX, baseados em metadados essenciais, também vem se consolidando, notadamente com os padrões europeus [ELI](https://en.wikipedia.org/wiki/European_Legislation_Identifier) e [ECLI](https://en.wikipedia.org/wiki/European_Case_Law_Identifier).

## Escopo

Apesar de não ser um elemento explícito na norma URN-LEX ou sua especialização LexML-URN, 
as URNs de matérias (separatas dos diários oficiais) podem ser agrupadas em grandes conjuntos:

* Poder Governamental (`gov`): subdividido em,

  * **Executivo** (`exe`): matérias emitidas por autoridades do Porder Executivo.
  * **Legislativo** (`leg`): matérias emitidas por autoridades do Porder Legislativo.
  * **Judiciário** (`jud`): matérias emitidas por autoridades do Porder Judiciário.
  * **Projetos** (`prj`): proposições e projetos de oficialização (tipicamente "projetos de Lei") de matérias emitidas pelo Legislativo ou Executivo.

* **Organizações** (`org`): associações, condomínios e sociedades anônimas também requerem publicação em Diário Oficial.

* **Modelos de contrato** (`mct`): de interesse misto (duas ou mais autoridades), que requerem publicação em Diário Oficial, e afetam ambos, `gov` e `org`,   de modo que são tratados de forma distinta, tais como as proposições normativas. Além de modelos de contrato, os termos de referência citados por contratos.

O *escopo* pode eventualmente se misturar dentro de um mesmo diário oficial, tipicamente matérias do Judiciário (ex. TRM) e do executivo são publicadas num mesmo diário, 
separadas eventualmente por seções.  De forma geral, todavia, os escopos são claros e sempre encontram-se publicados em meios (diários) separados.

## Data de publicação (ano)

Apesar de, na hierarquia do *path* URN LEX, a data de publicação da matéria (ano-mês-dia) ficar no final,  ela deve ser tomada como referência global para a interpretação dos demais metadados. 
Só a partir da data (em geral basta o ano) pode-se inferir a validade de um identificador de *autoridade* ou de *jurisdição*. O nome de um estado, por exemplo, depende do ano &mdash; o estado de Tocantins só passou a ser um nome válido a partir de 1988 (ver controle em [datasets-br/state-codes](https://github.com/datasets-br/state-codes/blob/master/data/br-state-codes.csv)), e o nome Guanabara deixou de ser válido em 1975.

Ficou convencionado portanto, no presente *dataset* e na resolução de nomes do [OFICIAL.NEWS](https://github.com/okfn-brasil/oficial.news), que a data de publicação tem precedência, estabelecendo o referencial de validação dos demais metadados.

## Terminologias controladas
Os metadados de jurisdição, autoridade e tipo-documento são relativos às URNs LEX canônicas, e portanto devem ser baseados em uma terminologia canônica. A versão 1 do conjunto de vocabulários LexML se encontra em http://dadosabertos.senado.leg.br/dataset/vocabul-rios-controlados-da-urn-lex 

### Jurisdições

As jurisdições são, a grosso modo, os limites geográficos de atuação das *autoridades*. 
Denominada na norma URN-LEX de *jurisdiction*, na sua definição sintática LexML-URN 
é também denominada [*local*](http://okfn-brasil.github.io/getlex/lexBr/#local). <br/>O arquivo da versão 1 original se encontra em http://www.lexml.gov.br/vocabulario/localidade.rdf.xml 

O arquivo [`jurisdicoes.csv`](jurisdicoes.csv) reúne todas as jurisdições previstas, com *URN LEX* respectivo nome oficial expresso por extenso.

O conceito tradicional das "esferas dos três poderes" (municipal, estadual e federal) reforça o uso 
do mapa  da divisão administrativa. Do ponto de vista de relevância quantitativa, essa é, de longe, 
a forma de jurisdição mais usada, bem documentada e amplamente aceita.

Ainda assim, no Brasil existem outras formas de parcelamento do território "para efeitos de jurisdição",
sendo a mais significativa a divisão oficial em bacias hidrográficas, ligada à autoridade dos [Comitês de Bacia](http://www.cbh.gov.br/). 
Há também a divisão por exemplo em territórios indígenas, que leva também a uma correlação geográfica de certas autoridades. 
Ambos exemplos demonstram que, *a priori*, nem sequer a hierarquia federal/estadual/municipal define, 
na escala geral (ex. mapas 1:50.000 ou menores), um mosaico único.  

A jurisdição portanto não pode ser tratada como um meio de classificação, com conjuntos disjuntos: existe a possibilidade 
de interseção espacial entre jurisdições. O que se oferece são regras (não-sintáticas)  "seletoras de mosaico", 
que garantem a independência (disjunção) das hierarquias jurisdição-autoridade. 

A estabilidade e consenso em torno de jurisdições deve ser analisada dentro de cada _escopo_. 
As convenções para se "brecar" uma hierarquia não são claras, 
requerendo que os curadores deste *dataset* tomem eventuais decisões relativas aos limites de hierarquização (tamanho do _path_ da jurisdição). 

Na esfera municipal, por exemplo, o Executivo de São Paulo e o IBGE adotaram em consenso a segmentação do território em 9 zonas, 
ao passo que o [TRT fixou 5 regiões](http://trt2.jus.br/indice-noticias-em-destaque/2320-trt-2-desenvolve-projeto-para-divisao-da-jurisdicao-de-sao-paulo) ([atualização](https://trt-2.jusbrasil.com.br/noticias/100378222/trt-2-desenvolve-projeto-para-divisao-da-jurisdicao-do-municipio-de-sao-paulo)).

NOTA: para a curadoria falta conferir por exemplo se a subdivisão municipal será mantida por zonas (subprefeituras como autoridades) ou alterado para distritos (subprefeituras como jurisdições). Quanto ao uso da sigla de UF, é uma extensão da sigla de país, presente na mesma norma ISO 3166-2, e já prevista na próxima versão do LEXML, e revista no [datasets-br/state-codes](https://github.com/datasets-br/state-codes).

### Autoridades
O arquivo da versão 1 original se encontra em http://www.lexml.gov.br/vocabulario/autoridade.rdf.xml 
...

Os arquivos `autoridades.csv` ocorrem repetidamente a cada _path_ de jurisdição nas pastas do presente dataset. 
Para evitar o uso de longos nomes e dificuldades de navegação, foram utilizadas as URN LEX abreviadas, conforme dataset `jurisdicao-abrev.csv`...

...


### Tipos de documento

O arquivo da versão 1 original se encontra em http://www.lexml.gov.br/vocabulario/tipoDocumento.rdf.xml 

...

