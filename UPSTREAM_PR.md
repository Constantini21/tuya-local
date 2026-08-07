# PR pronto para o upstream (make-all/tuya-local)

Abrir em: https://github.com/make-all/tuya-local/compare/main...Constantini21:tuya-local:m606-six-switch

**Título:** Add M606 six gang wall switch

**Corpo:**

Adds `wifi_m606_six_switch` for the M606 six gang wall switch (productKey `keyn5vwtmxgxfkjf`), the six-gang sibling of the existing M604 quad switch (`wifi_m604_quad_switch`), sharing its dp layout extended to six gangs:

- switches: dps 1-6 (boolean)
- countdown timers: dps 7-12 (integer, seconds)
- initial state: dp 14 (`power_off`/`power_on`/`last`)
- backlight: dp 16 (boolean)
- optional base64 schedule/inching blobs: dps 17-19 (same record formats documented in the M604 config; the ctrl byte extends to sw5 `0x09`/`0x08` and sw6 `0x0B`/`0x0A`)

Without this productKey listed, config matching falls back to the quad config and the device loses gangs 5 and 6.

Verified against the real device: tinytuya status returns `{1..6: bool, 7..12: int, 14: "memory", 16: bool}`, UDP discovery reports productKey `keyn5vwtmxgxfkjf`, protocol 3.3. Running in production on HA 2026.7.1 with all six gangs and timers reporting and controlling correctly.

DEVICES.md entry included.
