# EquationDeLaMort
 
Il s'agit d'une applet qui calcule le patrimoine restant en fonction de la durée de vie résiduelle (données INSEE 2020) sans revenus autres que la pension à un âge donné.

Il prend en compte l'inflation et les taux d'intérêts.

L'équation et le programme ont été élaboré par chatGPTo1-preview

```math
\boxed{C = P \times (1 + r{\prime})^{NR} - S_{\text{annuel}} \times \left[ \frac{(1 + r{\prime})^{NR} - (1 + i{\prime})^{NR}}{r{\prime} - i{\prime}} \right] + S_{\text{pension, annuel}} \times (1 + r{\prime})^{NR - t_1} \times \left[ \frac{(1 + r{\prime})^{t_2} - (1 + p{\prime})^{t_2}}{r{\prime} - p{\prime}} \right]}
```
avec:

i:inflation (i'=i/100)

r:taux d'intérêt

p:revalorisation annuelle des retraites

R:âge de départ à la retraite

A:âge actuel

S:montant prélevé chaque mois sur le capitil (or autres revenus)

Sp:montant intial pension

P:patrimoine initial