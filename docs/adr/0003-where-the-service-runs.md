# 0003. Where the service runs / Къде работи услугата

**Status / Статус:** Accepted

## Context / Контекст

The service needs a place to run that the whole team can reach and that we can automate in the next labs (Ansible, containers, CI/CD). The course gives us four lab servers: `web1`, `web2`, `db` and `lb` (`infra/servers`). / Услугата трябва да работи на място, достъпно за екипа, което можем да автоматизираме в следващите упражнения.

## Options / Варианти

1. **The lab servers: `web1` and `web2` behind `lb`, the database on `db`.** Pros: free, same for everyone, two app instances behind a load balancer, full control for Ansible. Cons: they run on our own machine, not reachable from the internet. / Плюсове: безплатни, еднакви за всички, две инстанции зад балансьор, пълен контрол. Минуси: не са достъпни от интернет.
2. **A cloud PaaS (e.g. Render, Fly.io).** Pros: public URL, managed TLS. Cons: needs an account and a card, hides the servers we want to learn to manage. / Плюсове: публичен адрес. Минуси: нужен акаунт, скрива сървърите.
3. **Only locally with `uvicorn`.** Pros: simplest. Cons: one instance, nothing to deploy to, no load balancing. / Плюсове: най-просто. Минуси: една инстанция, няма къде да внедряваме.

## Decision / Решение

The app runs on `web1` and `web2` on port 8000, `lb` forwards port 80 (8080 on the host) to them, and PostgreSQL runs on `db`. / Приложението работи на `web1` и `web2` на порт 8000, `lb` разпределя заявките, PostgreSQL е на `db`.

## Consequences / Последствия

- A request goes `lb` → `web1`/`web2` → `db`; one web server can fail without downtime. / Един уеб сървър може да падне без прекъсване.
- Deployment must update both web servers, which we automate with Ansible. / Внедряването обновява и двата сървъра с Ansible.
- The service is only reachable on our machine; a public deployment needs a new ADR. / Публично внедряване изисква ново решение.
