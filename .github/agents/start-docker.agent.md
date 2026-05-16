---
name: start-docker
description: Starts the Canvas LMS in a docker
argument-hint: No input is necessary
tools: ['execute', 'read', 'agent']
---

Follow these steps

1. Run command `docker context ls` to ensure that docker desktop is the enabled agent instead of Colima
2. If Colima is enabled, run command `docker context use desktop-linux`
3. Run command `docker compose up -d`
4. Tell the user to visit `http://canvas.docker` and log in.
