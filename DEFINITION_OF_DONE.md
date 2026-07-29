# Definition of Done — BarberHub MVP

A task/feature is **Done** only when **all** criteria below are met.

---

## 1. Code Complete

- [ ] All acceptance criteria from the Issue are implemented
- [ ] Code follows Coding Convention (naming, structure, lint)
- [ ] No dead code, commented-out code, or debug artifacts
- [ ] All `TODO` / `FIXME` in the diff are resolved or tracked as new issues
- [ ] PR contains only files relevant to the issue

---

## 2. Functional Correctness

- [ ] Feature works as specified in PRD / User Stories / RULES
- [ ] Acceptance Criteria from user story are met
- [ ] Edge cases handled (empty state, invalid input, boundary values)
- [ ] Business rules enforced (e.g. no double booking, tenant isolation)
- [ ] Error states return proper API format (`{success: false, message}`)
- [ ] Loading states shown during async operations
- [ ] API endpoints per **API Specification.md** (path, method, request/response shape)

---

## 3. Security & Access

- [ ] Auth required on protected endpoints (verified by test)
- [ ] Role-based access enforced (owner cannot access another tenant)
- [ ] Tenant isolation verified — tenant A cannot see tenant B's data
- [ ] Input validated & sanitized on all write endpoints
- [ ] SQL injection, XSS, CSRF vectors reviewed

---

## 4. Testing

### Backend (Laravel)
- [ ] Feature tests cover the happy path
- [ ] Feature tests cover at least 2 error/edge cases
- [ ] `php artisan test` passes (zero failures)

### Frontend (React)
- [ ] `npm run build` passes (zero errors)
- [ ] `npm run lint` passes (zero warnings)

---

## 5. Code Review

- [ ] PR reviewed by at least 1 other person
- [ ] All review comments resolved or acknowledged
- [ ] No merge conflicts with `master`
- [ ] CI pipeline passes (lint, typecheck, test, build)

---

## 6. Documentation

- [ ] API response format matches convention (no undocumented fields)
- [ ] If new ENV/config variable added, documented in `.env.example`
- [ ] Database migration reversible (`down` method provided)

---

## 7. API Completeness (per API Spec §18)

- [ ] All required endpoints available
- [ ] Authentication & authorization enforced
- [ ] Tenant isolation active on all business endpoints
- [ ] Input validation complete
- [ ] Error response format consistent
- [ ] Pagination on list endpoints

## 8. Deployability

- [ ] Docker build succeeds for affected service(s)
- [ ] No hardcoded environment-specific values (URLs, keys, secrets)
- [ ] `docker compose up -d --build <service>` starts clean

---

## 9. Git Hygiene

- [ ] Commit message follows convention: `type: description (closes #N)`
- [ ] Branch named: `type/nama-fitur-#<issue-number>`
- [ ] Branch rebased on latest `master` before merge
- [ ] Squash merge to `master`
- [ ] Branch deleted after merge
