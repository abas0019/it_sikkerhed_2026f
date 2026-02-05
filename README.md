Dette er et skoleprojekt på Zealand# it_sikkerhed_2026f
# Test strategier (IT-sikkerhed)

## Emne: Login til system (fx elbil-app eller portal)

Jeg tager udgangspunkt i et login-system, hvor en bruger skal kunne logge ind sikkert.
Jeg bruger følgende testteknikker:

---

## 1) Ækvivalensklasser (Equivalence Classes)

Regel: Password skal være mindst 8 tegn.

Ækvivalensklasser:
- 0-7 tegn -> ugyldigt password
- 8+ tegn -> gyldigt password

Eksempler:
- "1234567" -> afvist
- "12345678" -> godkendt

---

## 2) Grænseværditest (Boundary Value Testing)

Grænser for password-længde:
- 7 tegn -> afvist (lige under grænsen)
- 8 tegn -> godkendt (grænsen)
- 9 tegn -> godkendt (lige over grænsen)

---

## 3) CRUD(L) test

CRUD bruges til at teste funktionalitet for brugere i systemet.

Eksempel: Bruger-håndtering
- Create: Opret bruger
- Read: Se brugerprofil
- Update: Skift password / opdater e-mail
- Delete: Slet bruger
- (List): Se liste over brugere (admin)

---

## 4) Cycle process test

Eksempel: Password reset flow
1. Bruger trykker "Glemt password"
2. System sender reset-link
3. Bruger vælger nyt password
4. System opdaterer password
5. Bruger kan logge ind igen

Dette testes som en proces i flere trin, hvor man tjekker at hele flowet virker.

---

## 5) Test pyramiden

- Unit tests: Test af funktioner (fx password validering)
- Integration tests: Test af login mod database
- E2E tests: Test af hele login-flow i UI

Ideen er at have flest unit tests, færre integration tests og færrest E2E tests.

---

## 6) Decision table test (Beslutningstabel)

Login kan afhænge af flere regler.

Eksempel:
- Er brugernavn korrekt?
- Er password korrekt?
- Er brugeren låst (for mange forsøg)?

| Username korrekt | Password korrekt | Konto låst | Resultat |
|-----------------|------------------|-----------|----------|
| Ja              | Ja               | Nej       | Login OK |
| Ja              | Nej              | Nej       | Afvist   |
| Nej             | Ja               | Nej       | Afvist   |
| Nej             | Nej              | Nej       | Afvist   |
| Ja              | Ja               | Ja        | Afvist   |

---

## Security gates (hvor passer testene ind?)

- Unit tests (password længde, validering) -> Security Gate: Code / Unit test
- Integration tests (login mod database) -> Security Gate: Build / Integration
- E2E tests (login flow i UI) -> Security Gate: Release / Acceptance
- Decision table test -> Security Gate: Design / Requirements (regler skal være tydelige)
