# Select-MariaDB---PMSP
Select das questões para vaga de estágio.

-- 1. Quantos órgãos responderam à pesquisa, por ano?

SELECT COUNT(orgao) AS QtdOrgaos, ano_diagnostico FROM respostas_diagnostico
WHERE data_submissao is not NULL GROUP BY ano_diagnostico;


-- 2. Quantas pessoas trabalharam de forma dedicada à TI na Prefeitura de São Paulo, por ano?

SELECT SUM(qtd_equipe) AS PessoasTI, ano_diagnostico FROM respostas_diagnostico 
WHERE data_submissao is not NULL GROUP BY ano_diagnostico;

-- 3. Considerando que todas as pessoas que trabalharam de forma dedicada a TI receberam R$ 2.500,00/mês, qual a
proporção de custo com pessoal de TI por tipo de órgão, por ano?

select sum(qtd_equipe * 2500 * 12) as Custo,tipo_orgao,ano_diagnostico from respostas_diagnostico 
where tipo_orgao is not null AND data_submissao is not NULL group by tipo_orgao,ano_diagnostico 
ORDER BY ano_diagnostico;

-- 4. Quantos órgãos utilizam alguma metodologia para gerenciamento de projetos? Exiba graficamente:

SELECT COUNT(orgao) QtdOrgaos FROM respostas_diagnostico 
WHERE data_submissao is not NULL AND utiliza_metodologia > 0 and data_submissao is not NULL;

-- 5. Qual o total de computadores utilizados na Prefeitura de São Paulo, por ano? Exiba graficamente, escolhendo a
visualização que achar mais adequada:

SELECT SUM(desktop_proprio+desktop_locado),ano_diagnostico FROM respostas_diagnostico 
WHERE data_submissao is not NULL AND (desktop_proprio > 0 OR desktop_locado > 0) GROUP BY ano_diagnostico;


-- 6. Considerando que todos os computadores locados possuem menos de 5 anos de uso, qual é a proporção de
computadores que possuem mais de 5 anos e ainda são utilizados na Prefeitura de São Paulo, por ano? Exiba
graficamente, escolhendo a visualização que achar mais adequada.

SELECT SUM(desktop_proprio),SUM(desktop_proprio_antigo), ano_diagnostico FROM respostas_diagnostico 
WHERE data_submissao IS NOT NULL AND desktop_proprio > 0 GROUP BY ano_diagnostico;

-- 7. Considerando que os dados sobre quantidade de pessoas que trabalham dedicada à Tecnologia da Informação no
ano de 2019 apresenta a seguinte distribuição no ano de 2019, complete a frase que aparece abaixo dos
histogramas:
