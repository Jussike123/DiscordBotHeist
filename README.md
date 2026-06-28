<<<<<<< HEAD
# Discord ERLC Bot

Simple Discord bot for starting a Roblox location challenge and polling ERLC API for player arrival.

## Setup

1. Copy `config.example.json` to `config.json`.
2. Fill in `token`, `clientId`, `guildId`, `erlcApiBaseUrl`, `erlcApiKey`, `notifyDiscordId`, `boatApiBaseUrl`, and `boatApiToken`.
3. Use `http://127.0.0.1:8080` for `erlcApiBaseUrl` while testing with the mock server.
4. For live player location lookup, do not use `erlc.dev`.
   - `erlcApiBaseUrl` should be `https://api.erlc.gg`.
   - `erlcApiKey` should be your ER:LC server key, sent in the `server-key` header.
   - `erlc.dev` is only for server dashboard/event access and does not provide the live /location API.
4. Install dependencies with `pip install -r requirements.txt`.
5. Start the mock API server with `python mock_erlc_server.py`.
6. Start the bot with `python bot.py`.

## Mock API usage

While the mock server is running, set a player location with:

```powershell
python mock_erlc_server.py --host 127.0.0.1 --port 8080
```

Then, from another terminal:

```powershell
curl "http://127.0.0.1:8080/set-location?username=testuser&zipCode=205"
```

or on Windows PowerShell:

```powershell
Invoke-WebRequest -Uri "http://127.0.0.1:8080/set-location?username=testuser&zipCode=205"
```

To test the hint endpoint, use:

```powershell
curl -X POST "http://127.0.0.1:8080/send-hint" -H "Content-Type: application/json" -d "{\"username\":\"testuser\",\"hint\":\"START\"}"
```

or on Windows PowerShell:

```powershell
Invoke-RestMethod -Method Post -Uri "http://127.0.0.1:8080/send-hint" -ContentType "application/json" -Body '{"username":"testuser","hint":"START"}'
```

## Command

`/start username:<roblox username>`

`/location username:<roblox username>`

The bot randomly chooses one of two locations for `/start`:
- Pank (ZIP code 205)
- Bensukas (ZIP code 200)

`/location` returns the current player location data from the ERLC API. It will show coordinates, place name, or zip code depending on what the API returns.

The `/start` command polls the ERLC API for the player location for up to 10 seconds.

If the player arrives in time, the bot sends `Arrive` to the configured notify user.
If the attempt times out, the bot sends `fail`.

## New commands

`/kill target:<player>`

Sends an in-game kill command through the ERLC server command endpoint. If the target is omitted, the bot sends `:kill`.

`/kill1`

Kills all online players whose reported coordinates are inside the hard-coded kill zone around 2051 Freedom Avenue (x between 574.0 and 602.0, z between 2337.0 and 2361.0).
=======
# Discord ERLC Bot

Simple Discord bot for starting a Roblox location challenge and polling the ERLC API for player arrival.

## Features

- Start a location challenge with a slash command
- Poll the ERLC API for current player location data
- Notify a configured Discord user when the player arrives
- Support the mock ERLC server for local testing

## Setup

1. Copy `config.example.json` to `config.json`.
2. Fill in your Discord and ERLC values in `config.json`.
3. Keep your real secrets in your local `config.json`; it is ignored by Git and safe for private use while uploading the repository publicly.
4. Use `http://127.0.0.1:8080` for `erlcApiBaseUrl` while testing with the mock server.
5. For live player location lookup, do not use `erlc.dev`.
   - `erlcApiBaseUrl` should be `https://api.erlc.gg`.
   - `erlcApiKey` should be your ER:LC server key, sent in the `server-key` header.
   - `erlc.dev` is only for server dashboard/event access and does not provide the live /location API.
6. Install dependencies with `pip install -r requirements.txt`.
7. Start the mock API server with `python mock_erlc_server.py`.
8. Start the bot with `python bot.py`.

## Commands

- `/start username:<roblox username>`
- `/location username:<roblox username>`
- `/kill target:<player>`
- `/kill1`

## Mock API usage

While the mock server is running, set a player location with:

```powershell
python mock_erlc_server.py --host 127.0.0.1 --port 8080
```

Then, from another terminal:

```powershell
curl "http://127.0.0.1:8080/set-location?username=testuser&zipCode=205"
```

For the hint endpoint:

```powershell
curl -X POST "http://127.0.0.1:8080/send-hint" -H "Content-Type: application/json" -d "{\"username\":\"testuser\",\"hint\":\"START\"}"
```
>>>>>>> 0568330 (Clean public upload)
