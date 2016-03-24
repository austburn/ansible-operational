Handlers
--------
- Like regular tasks - but only ran in the task contains a `notify` directive
- Ex: If the nginx conf is changed, we probably want to restart nginx
    - Don't need to do this _all_ the time, only when it changes
- refer to handlers by name
```
# at the bottom of a play
handlers:
  - include: handlers/handlers.yml
```
