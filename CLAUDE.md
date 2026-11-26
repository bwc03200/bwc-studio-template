# CLAUDE.md

**Quick-start guide for Claude Code - Complete details in linked docs**

---

## Project Overview

bwc-studio-template — template de démarrage réutilisable pour les nouveaux
projets BWC Studio (Pierre Candille). Clone ce repo comme point de départ
pour chaque nouveau produit SaaS plutôt que de repartir de zéro.

**Tech Stack**: React + Vite + TypeScript, Supabase (backend/DB/auth),
Stripe, Playwright (E2E), bun (package manager) — adapte selon le projet

**Inclus dans `.claude/` (depuis ECC — github.com/affaan-m/ECC) :**
- `.claude/agents/` — 72 subagents spécialisés (review, sécurité, architecture...)
- `.claude/skills/` — 328 skills réutilisables (TDD, API design, patterns par stack...)
- `.claude/commands/` — 99 commandes
- `.claude/hooks-available/` — hooks ECC (auto-exec), **désactivés par défaut**.
  Voir `.claude/hooks-available/hooks.json` et `docs/ECC-security-guide.md`
  avant de les activer : ils s'exécutent automatiquement sur chaque action
  (Bash, Write, Edit, début/fin de session). Pour activer un hook précis,
  copie son entrée dans un `.claude/settings.json` plutôt que tout le fichier.
- `docs/ECC-README.md`, `docs/ECC-shortform-guide.md`, `docs/ECC-security-guide.md`
  — doc de référence ECC complète

**Skill `watch` (depuis claude-video — github.com/bradautomates/claude-video, MIT) :**
- `.claude/skills/watch/` — donne à Claude la capacité de "regarder" une vidéo
  (URL YouTube/TikTok/Vimeo ou fichier local) : téléchargement, extraction de
  frames, transcription, puis analyse par Claude. Invoquer via le skill `watch`.
- Deux moteurs : `gemini` (recommandé, nécessite une clé `GEMINI_API_KEY`
  gratuite sur https://aistudio.google.com/apikey) ou `local` (ffmpeg +
  yt-dlp + WhisperX/Groq/OpenAI en fallback, 100% local si besoin).
- Prérequis machine : Python 3.10+, ffmpeg/ffprobe, yt-dlp. Premier appel =
  setup interactif (`scripts/setup.py`) qui demande le moteur à utiliser.
- Un hook `SessionStart` (`.claude/hooks-active/scripts/watch/check-setup.sh`,
  lecture seule, toujours exit 0) avertit si Python/la config manque, sans
  jamais bloquer la session.
- Ne génère PAS de skill permanent à partir d'une vidéo automatiquement —
  c'est un outil d'analyse ponctuelle (malgré ce que certaines vidéos TikTok
  en disent).

---

## Session Start Protocol ⚡

**MANDATORY** at start of each session:

```bash
# Load essential docs (~800 tokens - 2 min read)
✓ .claude/COMMON_MISTAKES.md      # ⚠️ CRITICAL - Read FIRST
✓ .claude/QUICK_START.md          # Essential commands
✓ .claude/ARCHITECTURE_MAP.md     # File locations
```

**At task completion:**
- Create completion doc in `.claude/completions/YYYY-MM-DD-task-name.md`
- Move session file to `.claude/sessions/archive/` (if created)

**⚠️ NEVER auto-load:**
- Files in `.claude/completions/` (0 token cost)
- Files in `.claude/sessions/` (0 token cost)
- Files in `docs/archive/` (0 token cost)

---

## Quick Start Commands

```bash
# Add your common commands here
```

---

**Last Updated**: 2026-11-25
**Optimized with**: [Claude Token Optimizer](https://github.com/nadimtuhin/claude-token-optimizer)
