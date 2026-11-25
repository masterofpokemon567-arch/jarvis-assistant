# JARVIS 3.3 (stage 4)
Status: Android source has NOT been compiled or tested on a device.

## Build the APK
Option A: open this folder in Android Studio, then Build > Build APK.
Option B: upload all files (including the hidden .github folder) to a GitHub repository root. Open Actions > Build APK, and download the jarvis-apk artifact. Unzip and install on your phone (allow installs from that source).

## AI backend
Local check: `cd backend && pip install -r requirements.txt`, set GEMINI_API_KEY and JARVIS_TOKEN, run `uvicorn main:app`.
For the phone, deploy to an HTTPS Python host with start command `uvicorn main:app --host 0.0.0.0 --port $PORT` and the same variables. Use a long random token. Enter the address and token in the app's Settings. GEMINI_MODEL is optional.

## Test checklist
help, time, battery, torch on/off, volume up, open camera, open <app>, call 100 (dialer only), set timer 1 minute, set alarm 6:30 am, add task, restart app and show tasks, voice in en-IN and hi-IN, one AI question, wrong token shows error 401.

## Stage 2 tests
weather in Delhi, morning briefing, calculate (2+3)*4, note/show/delete note, remind me in 1 minute to stretch, add event exam, restart app and check chat, set wake to on and say "Jarvis time".

Optional web search: set GEMINI_SEARCH=1 on the backend. It may have its own quota or cost. Spoken replies include source links.

## Stage 3 tests
scan text (pick an English and a Hindi photo), notify me in 2 minutes to stretch (also with the app closed), create routine study: volume down; show tasks, then run study.

Reminders are approximate and are lost if the phone restarts or the app is force-stopped. Scanned text is read on the phone, but is kept in chat and may be sent to your AI server with later questions.

## Not yet built
Background wake word, reading other apps' notifications, scheduled routines, image/object understanding, calendar reading, task engine, smart home, Windows companion, encrypted storage, app login.

## Backend configuration
From the backend folder, copy .env.example to .env, fill it in, then run:
`uvicorn main:app --env-file .env`.
On a hosting service, set the same variables in its dashboard.

The phone app accepts only https addresses. `http://10.0.2.2:8000` and `http://<PC IP>:8000` will not work; use a hosted HTTPS URL (or an HTTPS tunnel to your PC).

## Build notes
No Gradle wrapper is included. The GitHub workflow installs Gradle 8.9 and JDK 17 and runs `gradle assembleDebug`.
Android Studio users may need to set the Gradle version to 8.9. The UI is Jetpack Compose, so there is no res/layout folder.

## Stage 4 tests
today's schedule and tomorrow's schedule (include an all-day event). Set lock to on, leave the app, return and unlock; also cancel the unlock.

App lock hides the app screen only. It does not encrypt data or hide reminder notifications, and does nothing if the phone has no screen lock.
