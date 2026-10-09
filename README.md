
Ce notebook construit un moteur d’analyse de risque de portefeuille en Python, avec téléchargement de prix historiques via Yahoo Finance, calcul des rendements, volatilité, Sharpe, drawdown, VaR et Expected Shortfall. Il simule aussi des scénarios de stress (2008, Covid, 2022) et un backtesting de la VaR via le test de Kupiec. Le portefeuille est diversifié avec des actions et ETF (SPY, QQQ, AAPL, NVDA, TLT, BND, GLD, etc.) et des poids fixes. Il analyse la corrélation entre actifs et la contribution de chacun au risque total. Il exporte ensuite les résultats sous forme de CSV/ZIP pour exploitation. En bref, c’est un outil de gestion quantitative du risque de portefeuille, très orienté finance quantitative et modélisation.

1. Quelle est l’action la plus volatile ?
NVIDIA (NVDA) est l’action la plus volatile du portefeuille, avec une volatilité annualisée de 51,7 %, selon les données du cours.
Cela signifie que ses rendements présentent des fluctuations particulièrement importantes par rapport aux autres actifs analysés.

2. La VaR passe-t-elle le backtesting ? (Test de Kupiec et système de feu tricolore)
Les résultats du test de Kupiec sont les suivants :
- VaR historique : p-value de 37,78 %.
- VaR paramétrique : p-value de 3,96 %.
- Niveau de confiance : 99 %.

Au seuil de significativité de 5 %, la VaR historique passe le test : on ne rejette pas l’hypothèse selon laquelle sa fréquence de dépassement est correcte.
En revanche, la VaR paramétrique ne passe pas le test au seuil de 5 %, puisque sa p-value de 3,96 % est inférieure à ce seuil.
Le système de feu tricolore de Bâle est indiqué comme « non applicable », car l’analyse porte sur 1 453 observations, alors que le cadre réglementaire standard repose sur 250 jours.

3. Comment la diversification évolue-t-elle lorsque les corrélations augmentent pendant une crise ?
En période de crise, les corrélations entre actifs risqués ont tendance à augmenter, ce qui réduit les bénéfices de la diversification.
Lorsque la corrélation commune atteint un niveau de stress de 95 %, la volatilité quotidienne du portefeuille passe de 1,10 % à 1,47 %.
Cette augmentation s’explique par le fait que les actifs évoluent davantage dans la même direction, ce qui limite leur capacité à compenser mutuellement leurs pertes.
La diversification devient donc moins efficace en période de crise, précisément lorsque la protection contre les pertes est la plus nécessaire.

4. Pourquoi la VaR historique et la VaR paramétrique sont-elles différentes ?
Les résultats obtenus sont :
- VaR historique : 29 215 $, soit 2,92 %.
- VaR paramétrique : 24 625 $, soit 2,46 %.
Cette différence provient des hypothèses utilisées par les deux méthodes.
La VaR historique repose sur les rendements réellement observés. Elle intègre donc les événements extrêmes, les asymétries et les queues épaisses présents dans les données financières.
La VaR paramétrique suppose généralement que les rendements suivent une distribution normale, ce qui peut conduire à sous-estimer les pertes extrêmes.
Dans cette analyse, la VaR historique est plus élevée parce qu'elle reflète des pertes extrêmes que le modèle normal capture moins bien.

5. Pourquoi la VaR Monte Carlo est-elle différente de la VaR historique ?
Les résultats sont les suivants :
- VaR Monte Carlo : 24 451 $, soit 2,45 %.
- VaR historique : 29 215 $, soit 2,92 %.
La méthode Monte Carlo génère un grand nombre de scénarios de rendements à partir d’une distribution statistique estimée.
Dans ce notebook, les simulations reposent sur une distribution normale multivariée, qui ne reproduit pas complètement les événements extrêmes observés historiquement.
C’est pourquoi la VaR Monte Carlo est proche de la VaR paramétrique, puisque les deux méthodes utilisent des hypothèses de distribution similaires.
La VaR historique reste plus élevée, car elle tient compte des pertes extrêmes effectivement observées sur les marchés.

6. Pourquoi l’Expected Shortfall est-il utile en complément de la VaR ?
La VaR mesure un seuil de perte associé à un niveau de confiance donné, mais elle ne renseigne pas sur la gravité des pertes lorsque ce seuil est dépassé.
L’Expected Shortfall (ES) mesure la perte moyenne dans les scénarios les plus défavorables.
À un niveau de confiance de 99 % :
- VaR historique : 2,92 %.
- Expected Shortfall historique : 4,08 %.
Ainsi, lorsque les pertes dépassent le seuil de VaR à 99 %, leur moyenne atteint environ 4,08 % du portefeuille.
L’Expected Shortfall permet donc de mieux évaluer les risques extrêmes et fournit une mesure complémentaire essentielle pour la gestion du risque.

7. Que se passe-t-il lorsque le portefeuille devient plus concentré ?
Une concentration plus importante sur des actifs volatils, comme NVIDIA (NVDA) ou l’ETF SOXX, augmente généralement le risque global du portefeuille.
Par exemple, NVIDIA représente seulement 10 % du portefeuille, mais contribue à 24,11 % de son risque total.
Cela montre qu’un actif peut avoir une contribution au risque largement supérieure à son poids financier.
Augmenter son exposition à ces actifs peut entraîner une hausse de la volatilité, des pertes potentielles plus importantes et des drawdowns plus profonds.
La concentration réduit donc les bénéfices de la diversification et rend le portefeuille plus vulnérable aux variations de quelques actifs dominants.

8. Quel est le pire scénario de stress et quel actif en est le principal responsable ?
Parmi les scénarios historiques analysés, la crise des marchés de 2022 représente le scénario le plus défavorable.
Les résultats sont :
- Perte du portefeuille : −29,34 %.
- Perte en valeur : −293 370 $.
- Principal contributeur aux pertes : NVIDIA (NVDA).
NVIDIA est particulièrement affectée par ce scénario et représente la contribution négative la plus importante au choc subi par le portefeuille.
En comparaison, le scénario hypothétique déterministe simulant une forte baisse des actions, avec notamment une chute de 50 % du SOXX, entraîne une perte de −21,50 %.
Le scénario historique de 2022 apparaît donc comme le plus sévère parmi les scénarios considérés.
