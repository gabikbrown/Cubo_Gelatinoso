![Imagem](Cabecalho.png)


# Criatura lendária: Cubo Gelatinoso

**Autora:** Gabriela O. de Lima Cabral\
**Professor:** Daniel Roberto Cassar\
**Ilum - Escola de ciência**\
**Centro Nacional de Pesquisa em Energia e Materiais (CNPEM)**

## Introdução e Objetivos
A doença arterial coronariana (DAC) é diagnosticada por exames invasivos e caros, como a angiografia. Este trabalho investiga a possibilidade de exames clínicos de rotina (pressão arterial, colesterol, eletrocardiograma, entre outros) já carregarem informação suficiente para indicar a doença, usando o algoritmo de k vizinhos mais próximos (*k-NN*) como classificador.

## Dados
**Fonte:** subconjunto húngaro do estudo Heart Disease, coletado no Instituto de Cardiologia de Budapeste e publicado no UCI Machine Learning Repository. Acesso feito por uma cópia hospedada no Kaggle

## Metodologia
**Divisão treino/teste:** holdout 80/20 sobre os índices do DataFrame, com semente fixa para reprodutibilidade: 208 pacientes de treino e 53 de teste.

**Baseline:** DummyClassifier, que responde sempre a classe majoritária ("sem doença"). Serve de régua: acurácia 69,81%, acurácia balanceada 50,00%.

**Métrica principal:** acurácia balanceada, que é a média entre sensibilidade e especificidade, por dar peso igual às duas classes mesmo com o alvo desbalanceado. 

## Experimentos e resultado
Foram avaliados 312 conjuntos de hiperparâmetros, organizados em três experimentos que isolam, cada um, o efeito de uma dessas decisões.

| Hiperparâmetro testado | Valores |
|---|---|
| Normalização | nenhuma, `MinMaxScaler`, `StandardScaler`, `MaxAbsScaler` |
| Codificação | `OneHotEncoder`, `OrdinalEncoder` |
| Número de vizinhos $k$ | 1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21, 25, 31 |
| Função de distância | Euclidiana, Manhattan, Chebyshev | 

Melhor conjunto: MaxAbsScaler + one-hot + k = 21 + distância Euclidiana: acurácia de 88,68% e acurácia balanceada de 86,57% no teste, contra 69,81% e 50% do baseline. O modelo identifica 13 dos 16 doentes do teste e 34 dos 37 saudáveis.

## Estrutura do repositório

```
.
- CuboGelationoso_GabrielaCabral.ipynb   # notebook principal: código, gráficos e discussão
- data.csv                                # conjunto de dados (baixar à parte, ver acima)
- 
- README.md
```
## Como executar
```bash
git clone <url-deste-repositório>
cd cubo-gelatinoso
pip install numpy pandas seaborn matplotlib scikit-learn
jupyter notebook CuboGelationoso_GabrielaCabral.ipynb
```

Com o `data.csv` na raiz do projeto, o notebook roda do início ao fim sem etapas manuais adicionais.
