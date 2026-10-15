# FIELDNOTES — Blog

A responsive editorial blog interface with article browsing, search/filter UI, individual article pages, and account/publishing screens.

## Pages

- `index.html` — article discovery and browsing.
- `singleblog.html` — individual article view.
- `addblog.html` — blog creation flow.
- `create.html` — sign-in screen.
- `auth.html` — account registration.
- `full.html` — expanded article/content view.

## Stack

- HTML, CSS and browser JavaScript
- Firebase Authentication
- Cloud Firestore
- Bootstrap styles on the authentication screen

## Run locally

Open `index.html` through a local static server (recommended) so browser module imports and Firebase requests behave consistently. For example, use VS Code Live Server or another static HTTP server.

## Firebase setup and security

The browser Firebase configuration identifies the Firebase project; it is not a substitute for security rules. Configure Firebase Authentication and Firestore rules in the Firebase console before accepting real users.

- Passwords must be handled only by Firebase Authentication. Never write passwords to Firestore.
- User profile documents should be keyed by the authenticated user's UID.
- Restrict profile reads/writes to the owning authenticated UID.
- Review article create/update/delete rules so only authorized authors can change content.
- Apply App Check and authorized-domain restrictions where appropriate.
- Do not put service-account credentials or private API secrets in browser code.

The signup handler stores only profile fields and a server timestamp. If an older version saved passwords in Firestore, treat those records as sensitive: remove the password fields and review access logs/rules. Do not reuse exposed passwords.

## Pre-release checklist

- [ ] Sign up with a new email; confirm duplicate-email and weak-password errors are understandable.
- [ ] Sign in and sign out; test invalid credentials and offline/network failure.
- [ ] Verify a profile document is written to `users/{uid}` without a password field.
- [ ] Test Firestore rules with two different accounts to confirm one user cannot read/write another user's profile.
- [ ] Create, view, edit and delete a post using the intended author permissions.
- [ ] Test search/filter, empty results, missing article IDs and refresh/deep links.
- [ ] Test mobile layout, keyboard navigation and reduced-motion preferences.

## Important

This repository has not been independently end-to-end tested as part of this documentation update. Verify the Firebase rules and all publishing flows in a test project before treating the app as production-ready.
