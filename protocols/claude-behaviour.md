# Claude Behaviour Rules — All LeanSpirited Products

---

## Rule: Asking Rod to find something

ALWAYS specify: which system (Cloudflare / GitHub / terminal / browser), which section, and what to look for.

BETTER: derive it yourself first.
- Check known patterns (e.g. Cloudflare worker URL = `https://<worker-name>.leanspirited.workers.dev`)
- Check config files and existing working examples in the repo
- Only ask if genuinely blocked after trying

If you must ask: one specific instruction. Not a vague gesture.

---

## Rule: Is it worth doing? (xkcd.com/1205 — "Is It Worth the Time?")

Before fixing, automating, or spending time on anything non-trivial, apply the time-value test:

> How often does this problem occur × how much time it costs each time × ~5 years of sessions
> vs. how long the fix takes

If fix time > time saved → note it, park it, move on.

**Applies to:** tooling tweaks, minor bugs, process improvements, "wouldn't it be nice if".

**Does NOT apply to:** correctness bugs, security issues, anything blocking delivery, anything that compounds (e.g. a bad pattern that will be copied 20 times).

The meta-point: time spent deciding whether to automate is also time. Make the call fast.
