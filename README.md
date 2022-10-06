# MJD

Trabalhos do Master em Jornalismo de Dados

Candidatos de Manaus não vacinados na cidade de Manaus

Este repositório contém o projeto final da disciplina "Fundamentos e Ética do Jornalismo de Dados", do curso Master de Jornalismo de Dados, Automação e Storytelling, do Insper. 

O grupo é formado por Arthur Cagliari (@arthurcagliari), Giseli Araujo (@GiseliAraujo), Lais (@laisbs0) Lucas Duarte (@) e Vinicius de Melo (@viniciusdmelo).

O grupo utilizou duas bases de dados para o trabalho. A primeira é fornecida pelo Tribunal Superior Eleitoral (TSE) e traz dados sobre os candidatos às vagas de deputado estadual, deputado federal, governador e presidente da República nas eleições de 2022. 

Esta primeira base tem dados desagregados por nome dos candidatos, cidade de origem, documento (CPF), partido e cargo postulante. O TSE fornece tais dados em documentos no formato CSV.

👨‍💻Notebook - Clique aqui para ler e baixar o arquivo.
✔CSV - Clique aqui para ler e baixar o arquivo.

A segunda base é disponibilizada pela Secretaria Municipal de Saúde do município de Manaus e apresenta dados de todas as pessoas vacinadas na cidade no período de 28 de agosto de 2021 a 21 de setembro de 2022. A secretaria fornece tais dados em documentos no formato PDF.

👨‍💻Notebook - Clique aqui para ler e baixar o arquivo.
✔CSV - Clique aqui para ler e baixar o arquivo.

O trabalho final buscava cruzar as duas bases e descobrir quais candidatos a cargos políticos em 2022, nascidos em Manaus, não tinham tomado a vacina na cidade neste período indicado pela tabela. Como o documento da Prefeitura de Manaus estavam disponibilizados em formato PDF, primeiro foi preciso fazer uma conversão do arquivo para algum outro formato em que se pudesse extrair os dados.

Quando utilizadas ferramentas gratuitas de conversores de arquivo PDF, não foi possível converter o documento como se esperava, conseguindo apenas trazer caracteres especiais. Assim, o grupo decidiu fazer uma coleta manual do arquivo PDF, página por página, selecionando o material desejado, copiando e depois colando em um arquivo TXT. 

Após isso, os dados foram tratados dentro do Excel, com a disponibilização das informações em colunas. Terminado esse tratamento, o documento foi importado para o SQL Server em tabela nomeada “Vacinados_AM”. Após a seleção da tabela, várias linhas ficaram sem a informação da faixa etária da pessoa vacinada, mas o documento final apresentou todos os números de CPF e também a data de vacinação –o que  já era suficiente para o trabalho de cruzamento planejado.

✔ CSV - clique aqui para ler e baixar o arquivo.
