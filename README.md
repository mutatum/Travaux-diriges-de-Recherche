# Comparaison des schémas numériques en volumes finis

Résultats visuels des schémas Rusanov, HLL, HLLC et Roe sur des cas tests de Riemann pour les équations d'Euler. Chaque GIF montre la performance des schémas sur les discontinuités. Organisation par cas test avec états initiaux en LaTeX (densité (\\rho), vitesse (u), pression (p)) et forces/faiblesses.

Les équations d'Euler en 1D s'écrivent : \[ \\frac{\\partial}{\\partial t} \\begin{pmatrix} \\rho \\ \\rho u \\ E \\end{pmatrix} + \\frac{\\partial}{\\partial x} \\begin{pmatrix} \\rho u \\ \\rho u^2 + p \\ u(E + p) \\end{pmatrix} = 0, \\quad E = \\frac{p}{\\gamma - 1} + \\frac{1}{2} \\rho u^2, \\quad \\gamma = 1.4 \] Discontinuité initiale à (x = 0.5).

## 1. Tube à choc de Sod

![Sod Shock Tube](sod_shock_tube_comparison.gif)
- **Test** : Onde de choc, onde de détente, contact.
- **États initiaux** : \[ \\text{Gauche : } (\\rho_L, u_L, p_L) = (1.0, 0.0, 1.0), \\quad \\text{Droite : } (\\rho_R, u_R, p_R) = (0.125, 0.0, 0.1) \]
- **Rusanov** : Simple, robuste, mais très diffusif, lisse les discontinuités.
- **HLL** : Moins diffusif, capture mieux les chocs, floute les contacts.
- **HLLC** : Précis sur contacts et chocs, bonne résolution.
- **Roe** : Très précis, mais peut violer l'entropie.

## 2. Contact stationnaire

![Static Contact HLL vs HLLC](static_contact_hll_vs_hllc_with_exact.gif)

![Static Contact Roe vs Roe No Entropy](static_contact_roe_vs_roe_no_entropy_with_exact.gif)

![Static Contact Comparison](static_contact_comparison.gif)
- **Test** : Discontinuité de contact immobile.
- **États initiaux** : \[ \\text{Gauche : } (\\rho_L, u_L, p_L) = (1.0, 0.0, 1.0), \\quad \\text{Droite : } (\\rho_R, u_R, p_R) = (0.5, 0.0, 1.0) \]
- **Rusanov** : Trop diffusif, mauvaise résolution du contact.
- **HLL** : Améliore la résolution, mais toujours flou.
- **HLLC** : Excellent pour les contacts stationnaires, netteté quasi-parfaite.
- **Roe** : Précis, mais oscillations possibles sans correction d'entropie.

## 3. Contact mobile

![Moving Contact HLL vs HLLC](moving_contact_hll_vs_hllc_with_exact.gif)

![Moving Contact Roe vs Roe No Entropy](moving_contact_roe_vs_roe_no_entropy_with_exact.gif)

![Moving Contact Shock](moving_contact_shock_comparison_20250601_1900.gif)
- **Test** : Contact en mouvement avec choc.
- **États initiaux** : \[ \\text{Gauche : } (\\rho_L, u_L, p_L) = (2.0, 1.0, 1.0), \\quad \\text{Droite : } (\\rho_R, u_R, p_R) = (1.0, 1.0, 1.0) \]
- **Rusanov** : Efface les chocs et contacts, perte de détails.
- **HLL** : Mieux sur les chocs, mais contacts flous.
- **HLLC** : Résout bien contacts et chocs, très fiable.
- **Roe** : Précis, mais sensible aux violations d'entropie.

## 4. Tests de Toro

### Toro Test 1

![Toro Test 1](toro_test_1_comparison_20250601_1859.gif)
- **États initiaux** : \[ \\text{Gauche : } (\\rho_L, u_L, p_L) = (1.0, 0.75, 1.0), \\quad \\text{Droite : } (\\rho_R, u_R, p_R) = (0.125, 0.0, 0.1) \]
- **Test** : Choc fort, contact, rarefaction.

### Toro Test 2

![Toro Test 2](toro_test_2_comparison.gif)
- **États initiaux** : \[ \\text{Gauche : } (\\rho_L, u_L, p_L) = (1.0, -2.0, 0.4), \\quad \\text{Droite : } (\\rho_R, u_R, p_R) = (1.0, 2.0, 0.4) \]
- **Test** : Ondes de détente symétriques.

### Toro Test 3

![Toro Test 3](toro_test_3_comparison.gif)
- **États initiaux** : \[ \\text{Gauche : } (\\rho_L, u_L, p_L) = (1.0, 0.0, 1000.0), \\quad \\text{Droite : } (\\rho_R, u_R, p_R) = (1.0, 0.0, 0.01) \]
- **Test** : Rarefaction forte.
- **Rusanov** : Stable mais floute tout, perte de précision.
- **HLL** : Meilleure capture des chocs, contacts faibles.
- **HLLC** : Équilibre précision/stabilité, bon sur tous les cas.
- **Roe** : Très précis, mais instable sans correction d'entropie.

## 5. Formation de vide

![Vacuum Riemann](vacuum_riemann_comparison_20250601_2047.gif)

![Roe Vacuum Formation](roe_vacuum_formation_comparison_20250601_2049.gif)
- **Test** : Régime de vide (rarefaction extrême).
- **États initiaux** : \[ \\text{Gauche : } (\\rho_L, u_L, p_L) = (1.0, -1.0, 0.4), \\quad \\text{Droite : } (\\rho_R, u_R, p_R) = (1.0, 1.0, 0.4) \]
- **Rusanov** : Robuste, mais mauvaise résolution des fronts.
- **HLL** : Gère bien les rarefactions, mais moins précis.
- **HLLC** : Bonne résolution, capture bien le vide.
- **Roe** : Très précis, mais peut diverger sans linéarisation adaptée.

## 6. Roe linéarisable vs non-linéarisable

### Roe linéarisable

![Roe Linearizable](roe_linearizable_roe_no_entropy_vs_roe_with_exact_20250601_2049.gif)
- **États initiaux** : \[ \\text{Gauche : } (\\rho_L, u_L, p_L) = (1.0, -0.5, 1.0), \\quad \\text{Droite : } (\\rho_R, u_R, p_R) = (1.0, 0.5, 1.0) \]
- **Test** : Linéarisation Roe valide, test de correction d'entropie.

### Roe non-linéarisable

![Roe Non-Linearizable](roe_non_linearizable_positive_comparison_20250601_2049.gif)
- **États initiaux** : \[ \\text{Gauche : } (\\rho_L, u_L, p_L) = (1.0, -\\sqrt{2}, 1.0), \\quad \\text{Droite : } (\\rho_R, u_R, p_R) = (1.0, \\sqrt{2}, 1.0) \]
- **Test** : Linéarisation Roe échoue, densité positive.
- **Roe** : Excellent sur cas linéarisables, mais échoue sans correction.

## 7. Onde de choc et rarefaction forte

![Collision Two Shocks](collision_two_shocks_comparison_20250601_2047.gif)

![Einfeldt Strong Rarefaction](einfeldt_strong_rarefaction_comparison_20250601_2047.gif)

![Einfeldt 123](einfeldt_123_comparison_20250601_2049.gif)

![Blast Wave](blast_wave_comparison.gif)
- **États initiaux (Collision Two Shocks)** : \[ \\text{Gauche : } (\\rho_L, u_L, p_L) = (1.0, 1.0, 1.0), \\quad \\text{Droite : } (\\rho_R, u_R, p_R) = (1.0, -1.0, 1.0) \]
- **États initiaux (Einfeldt Strong Rarefaction)** : \[ \\text{Gauche : } (\\rho_L, u_L, p_L) = (1.0, -1.0, 10^{-5}), \\quad \\text{Droite : } (\\rho_R, u_R, p_R) = (1.0, 1.0, 10^{-5}) \]
- **États initiaux (Einfeldt 123)** : \[ \\text{Gauche : } (\\rho_L, u_L, p_L) = (1.0, -2.0, 0.4), \\quad \\text{Droite : } (\\rho_R, u_R, p_R) = (1.0, 2.0, 0.4) \]
- **États initiaux (Blast Wave)** : \[ \\text{Gauche : } (\\rho_L, u_L, p_L) = (1.0, 0.0, 1000.0), \\quad \\text{Droite : } (\\rho_R, u_R, p_R) = (1.0, 0.0, 0.01) \]
- **Test** : Chocs multiples, rarefactions fortes.
- **Rusanov** : Stable mais très diffusif, détails perdus.
- **HLL** : Capture mieux les chocs, limite sur rarefactions.
- **HLLC** : Précis sur chocs et rarefactions, bon compromis.
- **Roe** : Très précis, mais instable sur rarefactions extrêmes.

## Synthèse

- **Rusanov** : Simple, stable, mais trop diffusif.
- **HLL** : Robuste, mieux sur chocs, faible sur contacts.
- **HLLC** : Meilleur équilibre, précis sur contacts et chocs.
- **Roe** : Très précis, mais nécessite corrections pour stabilité.