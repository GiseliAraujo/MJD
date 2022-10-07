# MJD

***TRABALHO DO MASTER EM JORNALISMO DE DADOS****

___Tema: Candidatos de Manaus não vacinados na cidade de Manaus___

Este repositório contém o projeto final da disciplina "Fundamentos e Ética do Jornalismo de Dados", do curso Master de Jornalismo de Dados, Automação e Storytelling, do Insper. 

O grupo é formado por [**Arthur Cagliari**](https://github.com/arthurcagliari), **[Giseli Araujo](https://github.com/GiseliAraujo)**, **[Lais Batista](https://github.com/laisbs0)**, **[Lucas Duarte](https://github.com/lucasduartematos)** e **[Vinicius de Melo](https://github.com/viniciusdmelo)**.

O grupo utilizou duas bases de dados para o trabalho. A primeira é fornecida pelo Tribunal Superior Eleitoral (TSE) e traz dados sobre os candidatos às vagas de deputado estadual, deputado federal, governador e presidente da República nas eleições de 2022. 

Esta primeira base tem dados desagregados por nome dos candidatos, cidade de origem, documento (CPF), partido e cargo postulante. O TSE fornece tais dados em documentos no formato CSV.

✔CSV - [Clique aqui](https://github.com/GiseliAraujo/MJD-FUNDAMENTOS-E-TICA-DO-JORNALISMO-DE-DADOS/blob/main/consulta_cand_2022_AM.xlsx) para ler e baixar o arquivo.

A segunda base é disponibilizada pela Secretaria Municipal de Saúde do município de Manaus e apresenta dados de todas as pessoas vacinadas na cidade no período de 28 de agosto de 2021 a 21 de setembro de 2022. A secretaria fornece tais dados em documentos no formato PDF.

✔ PDF - Clique nos links para ler e baixar os arquivos ([parte 1](https://www2.manaus.am.gov.br/docs/semsa/Lista%2011-06-2021.pdf), [parte 2](https://www2.manaus.am.gov.br/docs/semsa/Vacinados_2022-10-06_as_19h00min.pdf), [parte 3](https://www2.manaus.am.gov.br/docs/semsa/Vacinados_2021-08-27_as_19h00min%20(1).pdf), [parte 4](https://www2.manaus.am.gov.br/docs/semsa/Vacinados_2021-07-07_as_19h00min.pdf))
OBS: Os arquivos originais não foram subidos no GitHub por serem maior que 25 MB.

O trabalho final buscava cruzar as duas bases e descobrir quais candidatos a cargos políticos em 2022, nascidos em Manaus, não tinham tomado a vacina na cidade neste período indicado pela tabela. Como o documento da Prefeitura de Manaus estava disponibilizado em formato PDF, primeiro foi preciso fazer uma conversão do arquivo para algum outro formato em que se pudesse extrair os dados.

Quando utilizadas ferramentas gratuitas de conversores de arquivo PDF, não foi possível converter o documento como se esperava, conseguindo apenas trazer caracteres especiais. Assim, o grupo decidiu fazer uma coleta manual do arquivo PDF, página por página, selecionando o material desejado, copiando e depois colando em um arquivo TXT. 

Após isso, os dados foram tratados dentro do Excel, com a disponibilização das informações em colunas. Terminado esse tratamento, o documento foi importado para o SQL Server em tabela nomeada “Vacinados_AM”. Após a seleção da tabela, várias linhas ficaram sem a informação da faixa etária da pessoa vacinada, mas o documento final apresentou todos os números de CPF e também a data de vacinação –o que  já era suficiente para o trabalho de cruzamento planejado.

✔ CSV - Clique nos links para ler e baixar os arquivos ([parte 1](https://github.com/GiseliAraujo/MJD-FUNDAMENTOS-E-TICA-DO-JORNALISMO-DE-DADOS/blob/main/Primeiro.xlsx), [parte 2](https://github.com/GiseliAraujo/MJD-FUNDAMENTOS-E-TICA-DO-JORNALISMO-DE-DADOS/blob/main/Segundo.xlsx), [parte 3](https://github.com/GiseliAraujo/MJD-FUNDAMENTOS-E-TICA-DO-JORNALISMO-DE-DADOS/blob/main/terceiro.xlsx), [parte 4](https://github.com/GiseliAraujo/MJD-FUNDAMENTOS-E-TICA-DO-JORNALISMO-DE-DADOS/blob/main/Quarto.xlsx))

***#CONTEXTO DO TEMA***

O grupo escolheu cruzar tais dados sobre candidatos não vacinados na cidade de Manaus, pois a capital amazonense ganhou repercussão internacional com a falta de oxigênio e o uso de medicamentos reconhecidamente ineficazes para o tratamento da covid-19 durante a pandemia. Daí o interesse em saber se atores que estavam se postulando a um cargo político não teriam deixado de tomar a vacina. A partir de tais nomes, o grupo seguiria uma investigação mais aprofundada sobre essas pessoas.

***#PERGUNTAS***

___1 - Há quantos candidatos no estado do Amazonas?___

660 (sendo eles Aptos e Inaptos)

```
   SELECT Count(nm_candidato)
     FROM candidatos2022
```
___2 - Quantos candidatos do estado do Amazonas não se vacinaram em Manaus?___

130 Candidatos

```
SELECT Count(c.Nr_cpf_candidato)
  FROM candidatos2022 AS C
 WHERE SG_UF_NASCIMENTO = 'AM'
   AND NOT EXISTS (SELECT *
                     FROM [Vacinados_AM]
                    WHERE CPF = c.Nr_cpf_candidato)                 
                    
```

___3 - Quais candidatos do estado do Amazonas não se vacinaram em Manaus?___

✔ Abrir o arquivo deste projeto com o nome  -- >> NãoVacinadosNascidosManaus.xls

```
SELECT  c.Nr_cpf_candidato, 
				c.nm_candidato, 
				c.DS_Cargo, 
				c.SG_Partido ,
				CD_TIPO_ELEICAO,
				NM_TIPO_ELEICAO,
				NR_TURNO,
				CD_ELEICAO,
				DS_ELEICAO,
				DT_ELEICAO,
				TP_ABRANGENCIA,
				SG_UF,
				SG_UE,
				NM_UE,
				CD_CARGO,
				DS_CARGO,
				SQ_CANDIDATO,
				NR_CANDIDATO,
				NM_CANDIDATO,
				NM_URNA_CANDIDATO,
				NM_SOCIAL_CANDIDATO,
				NR_CPF_CANDIDATO,
				NM_EMAIL	,
				CD_SITUACAO_CANDIDATURA,
				DS_SITUACAO_CANDIDATURA,
				CD_DETALHE_SITUACAO_CAND,
				DS_DETALHE_SITUACAO_CAND,
				TP_AGREMIACAO,
				NR_PARTIDO,	
				SG_PARTIDO,	
				NM_PARTIDO,	
				NR_FEDERACAO,	
				NM_FEDERACAO,	
				SG_FEDERACAO,
				DS_COMPOSICAO_FEDERACAO,
				SQ_COLIGACAO,
				NM_COLIGACAO,
				DS_COMPOSICAO_COLIGACAO	,
				CD_NACIONALIDADE,	
				DS_NACIONALIDADE,
				SG_UF_NASCIMENTO,
				CD_MUNICIPIO_NASCIMENTO,
				NM_MUNICIPIO_NASCIMENTO,
				DT_NASCIMENTO,
				NR_IDADE_DATA_POSSE,
				NR_TITULO_ELEITORAL_CANDIDATO,
				CD_GENERO,
				DS_GENERO,
				CD_GRAU_INSTRUCAO,
				DS_GRAU_INSTRUCAO,
				CD_ESTADO_CIVIL,
				DS_ESTADO_CIVIL	,
				CD_COR_RACA,
				DS_COR_RACA	,
				CD_OCUPACAO,
				DS_OCUPACAO,
				VR_DESPESA_MAX_CAMPANHA,
				CD_SIT_TOT_TURNO,
				DS_SIT_TOT_TURNO,
				ST_REELEICAO,
				ST_DECLARAR_BENS,
				NR_PROTOCOLO_CANDIDATURA,
				NR_PROCESSO	CD_SITUACAO_CANDIDATO_PLEITO,
				DS_SITUACAO_CANDIDATO_PLEITO,
				CD_SITUACAO_CANDIDATO_URNA,
				DS_SITUACAO_CANDIDATO_URNA,	
				ST_CANDIDATO_INSERIDO_URNA	,
				NM_TIPO_DESTINACAO_VOTOS,	
				CD_SITUACAO_CANDIDATO_TOT,	
				DS_SITUACAO_CANDIDATO_TOT,	
				ST_PREST_CONTAS

 FROM  candidatos2022 AS C
WHERE SG_UF_NASCIMENTO = 'AM'
  AND NOT EXISTS (SELECT * 
                    FROM [Vacinados_AM]
                   WHERE CPF = c.Nr_cpf_candidato)
```
___4 - Há candidatos do Amazonas para presidência ou governador do estado que não se vacinaram em Manaus? Quantos?___

R.Não tem candidatos a Presidencia e 2 para Governadores(AMAZONINO ARMANDO MENDES e NAIR QUEIROZ BLAIR)

``` 

SELECT * 
  FROM candidatos2022 AS C
 WHERE DS_CARGO IN ('GOVERNADOR', 'PRESIDENTE')
   AND NOT EXISTS (SELECT *
                     FROM [Vacinados_AM]
                    WHERE CPF = c.Nr_cpf_candidato)  
 
 ```
    
___5 - Quantos candidatos no estado do Amazonas nasceram em Manaus?___

R. 38 candidatos.


``` 
--Quantos candidatos

SELECT  COUNT(* )
FROM  candidatos2022 AS C
WHERE NM_MUNICIPIO_NASCIMENTO = 'MANAUS'

--Quem são os candidatos nascidos em Manaus?

SELECT  * 
FROM  candidatos2022 AS C
WHERE NM_MUNICIPIO_NASCIMENTO = 'MANAUS'

``` 
 
___6 - Qual é o partido predominante dos candidatos nascidos em Manaus e não vacinados em Manaus?____

![image](https://user-images.githubusercontent.com/114266007/194380275-e92f6fe1-cc07-45eb-bc99-8be31a282c1e.png)

``` 
SELECT COUNT(SG_PARTIDO ), SG_PARTIDO
  FROM candidatos2022 AS C
 WHERE SG_PARTIDO
 GROUP BY SG_PARTIDO
 ``` 


___7 - Há muitos candidatos indígenas nascidos em Manaus e não vacinados em Manaus?___

R. 1 candidata, ANA CLAUDIA MARTINS TOMAS

 ``` 
-- Contar a quantidade de candidatos que são indigenas

SELECT Count(* )
  FROM candidatos2022 AS C
 WHERE DS_COR_RACA = 'INDÍGENA'

 -- Quem são os candidatos indigenas ?

SELECT *
  FROM candidatos2022 AS C
 WHERE DS_COR_RACA = 'INDÍGENA'
  ``` 

___8 - Qual era a cor/raça predominante dos candidatos nascidos em Manaus?___

![image](https://user-images.githubusercontent.com/114266007/194381013-61547351-51ec-4241-ab61-a9dbd77a2e63.png)


R. De acordo com os dados, 47 candidatos não-vacinados em Manaus se autodeclaram pardos. Esse número é 840% maior do que o número de candidatos indígenas (5), que  tem o menor número de autodeclarados. Os pardos representam 54,02% dos candidatos nas eleições gerais de 2022.

  ``` 
SELECT Count(* ) , DS_COR_RACA
  FROM candidatos2022 AS C
  GROUPY BY DS_COR_RACA
    ``` 

___Caminhos possíveis a serem seguido para realização de pauta, com os insights obtidos por meio da análise de dados:___

1. Confirmar quais candidatos nascidos em Manaus realmente não tomaram vacina contra Covid-19 e cruzar com sua atuação durante a pandemia. Quem não tomou vacina foi considerado negacionista? Incentivou o uso de cloroquina e tratamento precoce? Preconizou contra a origem das vacinas, principalmente a Coronavac? Sua posição política é alinhada com o governo?

2. Quem são os políticos não-vacinados dos partidos com maior número de não-vacinados (Agir, PDT e Solidariedade) em Manaus? Qual o alinhamento político de cada um desses candidatos? Eles defenderam o tratamento precoce e o uso da cloroquina? Em caso de políticos que concorriam a eleição, destinaram verbas ou promoveram políticas públicas em prol de outros tratamentos que não a vacinação contra a Covid-19?

3. A candidata indígena Ana Claudia Martins Tomas não tomou a vacina em Manaus. Ela realmente não foi vacinada? Se sim, quais as alegações? Lembrar-se que houve uma rejeição à vacinação por parte da população indígena devido a influência das comunidades evangélicas.
