<wizard-report>
# PostHog post-wizard report

The wizard has completed a deep integration of PostHog into the Skild TanStack Start project. Here's a summary of what was done:

- **`posthog-js`** installed as a project dependency.
- **Environment variables** (`VITE_PUBLIC_POSTHOG_PROJECT_TOKEN`, `VITE_PUBLIC_POSTHOG_HOST`) written to `.env.local`.
- **`PostHogProvider`** added in `src/routes/__root.tsx`, wrapping the entire app so all routes have access to PostHog.
- **User identification** added via a `PostHogUserIdentifier` component inside `ClerkProvider` in `__root.tsx`. It uses Clerk's `useUser` hook to call `posthog.identify()` whenever the authenticated user changes, and `posthog.reset()` on sign-out.
- **Exception capture** enabled via `capture_exceptions: true` in the PostHog provider options.
- **Reverse proxy** configured in `vite.config.ts` — all PostHog requests route through `/ingest` to avoid ad blockers.
- **5 events** instrumented across 2 files (see table below).

| Event | Description | File |
|---|---|---|
| `browse_registry_clicked` | User clicks the Browse Registry CTA on the homepage hero — top of skill discovery funnel | `src/routes/index.tsx` |
| `publish_skill_clicked` | User clicks the Publish Skill CTA on the homepage — top of skill publishing funnel | `src/routes/index.tsx` |
| `skill_install_command_copied` | User copies a skill's install command — strongest signal of install intent | `src/components/SkillCard.tsx` |
| `skill_opened` | User clicks Open on a skill card to view skill details | `src/components/SkillCard.tsx` |
| `skill_upvoted` | User upvotes a skill on the registry listing | `src/components/SkillCard.tsx` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- **Dashboard — Analytics basics**: https://us.posthog.com/project/387921/dashboard/1484077
- **Registry → Install Intent Funnel**: https://us.posthog.com/project/387921/insights/RwA6ll23
- **Install Command Copies Over Time**: https://us.posthog.com/project/387921/insights/HHR0eS4J
- **Homepage CTAs — Browse vs Publish**: https://us.posthog.com/project/387921/insights/rSbbMIYt
- **Skill Engagement — Opens & Upvotes**: https://us.posthog.com/project/387921/insights/s1JKrbNL
- **Publish Skill → Install Command Funnel**: https://us.posthog.com/project/387921/insights/88xNEf5m

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.

</wizard-report>
