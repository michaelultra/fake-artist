# Fake Artist

A tiny companion app for playing *A Fake Artist Goes to New York* over Zoom. The host clicks **Next Game**; everyone sees the same category, everyone but one player sees the same word, and one player sees **FAKE**. The same player is never the fake two rounds in a row.

Live: https://michaelultra.github.io/fake-artist/

## How it works

- Static page on GitHub Pages: `index.html` plus a vendored copy of [mqtt.js](https://github.com/mqttjs/MQTT.js) 5.10.1.
- Shared state goes through the free public EMQX broker (`wss://broker.emqx.io:8084/mqtt`) as retained MQTT messages under `ultra-fakeartist/v1/<ROOM>/`, so late joiners and page refreshes pick up the current round.
- The host's browser is the dealer. It keeps the current answer and the last fake in its own localStorage.
- No logins. Players are identified by a random id saved in their browser.

The public broker is open, so this keeps casual players honest but isn't secure against someone who goes looking for the messages.

## Local testing

Serve the folder (`python3 -m http.server`) and open `?room=CODE&p=2`, `&p=3` and so on in extra tabs to act as separate players in one browser.
