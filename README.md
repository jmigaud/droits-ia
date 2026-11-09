# droits-ia

Assistant IA qui trouve les aides auxquelles un foyer a droit sans le savoir, prépare les dossiers et suit les échéances jusqu'au versement.

- Plan détaillé (document vivant) : https://claude.ai/artifact/JXjhYYpq9oBkDRezTmT51H
- Suivi des tâches : onglet **Issues** (une issue par action, un milestone par phase)

## Critères de réussite

| Critère | Objectif |
| --- | --- |
| Temps pour un bilan complet | < 10 minutes |
| Écart avec les simulateurs officiels | < 5 % |
| Testeurs qui découvrent au moins une aide | ≥ 1 sur 3 |
| Dossiers réellement déposés après le bilan | ≥ 50 % |

## Architecture

```
Utilisateur → Assistant IA (dialogue, lecture de documents) → Fiche du foyer (validée)
           ↑                                                        ↓
   validation et envoi  ←  Résultats et dossiers  ←  OpenFisca (calcul officiel)
```

## Structure

| Dossier | Contenu |
| --- | --- |
| `backend/` | API FastAPI : OpenFisca-France + API Claude |
| `frontend/` | Interface React (PWA) |
| `tests/foyers/` | Foyers fictifs de référence (JSON) pour vérifier les calculs |
| `sources/` | Études, textes de loi et références |

## Règles du projet

- L'IA ne calcule jamais un montant elle-même : tout vient d'OpenFisca.
- On ne stocke jamais les identifiants CAF, impôts ou autres. L'utilisateur dépose lui-même.
- Minimum de données personnelles, documents supprimés après lecture, hébergement UE.
- Premier territoire test : Charente / Angoulême.
