# PRD — Prompt2Agent

> Un skill universel pour IDE IA qui transforme `/Prompt2Agent <prompt>` en agent complet prêt à déployer.

**Statut :** En développement  
**Version :** 0.1.0  
**Auteur :** Erwan Sagnardon ([@erwancodes](https://github.com/erwancodes))  
**Licence :** MIT  
**Site :** [prompt2agent.dev](https://prompt2agent.dev)  
**Date :** 28 avril 2026

---

## 1. Vue d'ensemble

Prompt2Agent est un skill open source installable en une commande pour les IDE IA (Claude Code, Cursor, Codex). Une fois installé, le développeur peut taper `/Prompt2Agent <description>` directement dans son IDE et obtenir instantanément un agent IA complet : system prompt optimisé, config JSON, et code d'intégration pour OpenAI, Anthropic et LangChain.

Aucune clé API externe, aucun backend. C'est l'IA de l'IDE qui fait le travail à partir des instructions du skill.

Le projet comprend deux parties :

1. **Le skill** : un fichier markdown d'instructions installable via `npx skills add`
2. **La landing + docs** : un site Vite + shadcn/ui sur `prompt2agent.dev`

---

## 2. Problème

Configurer un agent IA from scratch prend du temps et demande de la connaissance. Un développeur doit :

- Structurer un system prompt efficace
- Choisir les bons paramètres (température, max_tokens, tools...)
- Adapter le code selon le framework cible (OpenAI, Anthropic, LangChain...)
- Répéter ce processus pour chaque nouveau projet

Prompt2Agent automatise entièrement cette étape directement dans l'environnement de développement du dev, sans quitter son IDE.

---

## 3. Solution

### 3.1 Le skill

Un fichier markdown contenant des instructions précises pour l'IA de l'IDE. Quand le développeur tape `/Prompt2Agent <description de l'agent>`, le skill guide l'IA pour générer :

- Un **system prompt** optimisé et structuré
- La **config JSON** complète (modèle, température, max_tokens, tools recommandés)
- Le **code d'intégration** pour OpenAI, Anthropic et LangChain
- Un **exemple de premier message utilisateur**

### 3.2 La landing page

Un site simple sur `prompt2agent.dev` qui présente le projet, explique comment installer le skill et documente les outputs générés.

---

## 4. Cible utilisateur

**Profil principal :** Développeur qui utilise Claude Code, Cursor ou Codex au quotidien et veut bootstrapper un agent IA rapidement sans quitter son IDE.

**Profil secondaire :** Développeur débutant avec les agents IA qui a besoin d'un point de départ structuré et d'une documentation claire.

---

## 5. Fonctionnalités

### 5.1 Le skill (core)

| Fonctionnalité | Description | Priorité |
|---|---|---|
| Commande `/Prompt2Agent` | Déclenche la génération depuis n'importe quel IDE IA | P0 |
| Output OpenAI | Config + code d'intégration pour l'API OpenAI | P0 |
| Output Anthropic | Config + code pour l'API Anthropic Claude | P0 |
| Output LangChain | Code Python pour LangChain | P0 |
| System prompt optimisé | Prompt structuré avec rôle, contexte, contraintes | P0 |
| Tools recommandés | Liste des tools pertinents selon la description | P1 |
| Fichier de sortie | Génère un fichier `agent.md` dans le projet | P1 |

### 5.2 La landing page

| Fonctionnalité | Description | Priorité |
|---|---|---|
| Hero section | Présentation du projet + commande d'install | P0 |
| Demo visuelle | Exemple de `/Prompt2Agent` en action (code animé) | P0 |
| Documentation | Explication des outputs générés par framework | P0 |
| Quick start | Guide d'installation en 3 étapes | P0 |
| Section GitHub | Lien vers le repo + badge stars | P1 |
| Mode sombre | Dark mode par défaut | P1 |

### 5.3 Post-MVP (v0.2+)

| Fonctionnalité | Description | Priorité |
|---|---|---|
| Support CrewAI | Ajout d'un 4e framework cible | P2 |
| Support AutoGen | Ajout Microsoft AutoGen | P2 |
| Templates | Exemples de prompts par catégorie (support, SEO, code review...) | P2 |
| Flag `--framework` | `/Prompt2Agent --framework openai <prompt>` pour cibler un seul framework | P2 |

---

## 6. Structure du projet

```
prompt2agent/
├── skill/
│   └── prompt2agent.md        # Le skill principal (instructions pour l'IA)
│
├── landing/                   # Site Vite + shadcn/ui
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── ui/            # Composants shadcn
│   │   │   ├── Hero.jsx       # Hero section avec commande d'install
│   │   │   ├── Demo.jsx       # Démo visuelle animée
│   │   │   ├── HowItWorks.jsx # Guide 3 étapes
│   │   │   ├── Docs.jsx       # Documentation des outputs
│   │   │   └── Footer.jsx
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── index.css
│   ├── index.html
│   ├── vite.config.js
│   ├── tailwind.config.js
│   └── package.json
│
├── examples/                  # Exemples d'outputs générés
│   ├── support-agent.md
│   ├── code-review-agent.md
│   └── seo-agent.md
│
├── README.md
├── LICENSE
└── package.json               # Pour npx skills add
```

---

## 7. Le skill — contenu de `prompt2agent.md`

Le fichier skill contient les instructions suivantes pour l'IA de l'IDE :

```markdown
# Prompt2Agent Skill

## Trigger
Quand l'utilisateur tape `/Prompt2Agent <description>`, génère un agent IA complet.

## Instructions
Tu es un expert en architecture d'agents IA.
À partir de la description fournie, génère les éléments suivants :

### 1. System Prompt
Un system prompt complet avec :
- Le rôle précis de l'agent
- Le contexte d'utilisation
- Les contraintes et limites
- Le ton et le style attendu

### 2. Configuration
Pour chaque framework, génère :
- Le modèle recommandé
- La température adaptée au cas d'usage
- Le max_tokens approprié
- La liste des tools pertinents

### 3. Code d'intégration
Génère le code prêt à l'emploi pour :
- OpenAI (Python ou JavaScript selon le projet détecté)
- Anthropic Claude (Python ou JavaScript selon le projet détecté)
- LangChain (Python)

### 4. Fichier de sortie
Crée un fichier `agent.md` dans le dossier courant avec tout le contenu généré,
organisé en sections claires et copiables.
```

---

## 8. Installation et utilisation

### Installation (commande unique)

```bash
npx skills add https://github.com/erwancodes/prompt2agent
```

Le package détecte automatiquement l'IDE utilisé et place le skill au bon endroit :

| IDE | Dossier cible |
|---|---|
| Claude Code | `.claude/commands/` |
| Cursor | `.cursor/rules/` |
| Codex | `.codex/skills/` |

### Utilisation

```bash
/Prompt2Agent Un assistant qui aide les développeurs à reviewer leur code Python
```

### Output attendu

L'IA génère et crée un fichier `agent.md` contenant :

```
## System Prompt
...

## Config OpenAI
...

## Config Anthropic
...

## Config LangChain
...

## Tools recommandés
...

## Exemple de premier message
...
```

---

## 9. Stack technique

### Skill
| Élément | Choix |
|---|---|
| Format | Markdown (`.md`) |
| Distribution | `npx skills add` |
| Compatibilité | Claude Code, Cursor, Codex |

### Landing page
| Élément | Choix |
|---|---|
| Framework | React 19 + Vite |
| UI | shadcn/ui + Tailwind CSS |
| Thème | Dark mode par défaut |
| Déploiement | Vercel |
| Domaine | prompt2agent.dev |

---

## 10. Flux utilisateur complet

```
1. Le développeur visite prompt2agent.dev et découvre le projet

2. Il installe le skill en une commande :
   npx skills add https://github.com/erwancodes/prompt2agent

3. Le skill est placé automatiquement dans le bon dossier selon l'IDE détecté

4. Dans son IDE, il tape :
   /Prompt2Agent <description de l'agent>

5. L'IA de l'IDE lit les instructions du skill et génère :
   - Le system prompt optimisé
   - La config JSON par framework
   - Le code d'intégration (OpenAI / Anthropic / LangChain)

6. Un fichier agent.md est créé dans le projet avec tout le contenu

7. Le développeur copie ou adapte le code généré directement dans son projet
```

---

## 11. Contraintes et limites

- Le skill dépend de l'IA de l'IDE. La qualité du résultat dépend du modèle utilisé par le développeur.
- La détection automatique de l'IDE via `npx skills add` doit couvrir les 3 cibles principales (Claude Code, Cursor, Codex).
- Le site landing est entièrement statique, aucun backend requis.
- Le skill est en anglais pour maximiser la portée internationale.

---

## 12. Métriques de succès

| Métrique | Objectif v0.1 |
|---|---|
| Stars GitHub | 100+ dans le premier mois |
| Installs `npx skills add` | 50+ dans le premier mois |
| Compatibilité IDE | Claude Code + Cursor + Codex |
| Qualité des outputs | Testée manuellement sur 20 cas différents |

---

## 13. Roadmap

```
Avril 2026   — PRD finalisé
Mai 2026     — Développement du skill + landing page
Juin 2026    — Publication open source sur GitHub + prompt2agent.dev live
Juillet 2026 — Retours communauté + v0.2 (CrewAI, templates, flags)
```

---

*Prompt2Agent est un projet open source développé sous Helionis Labs.*
