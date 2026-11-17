# Screen Helper Privacy Policy

**App:** Screen Helper (螢幕小幫手)  
**Publisher:** FusionCore  
**Effective date:** 17 November 2026  
**Contact:** bump.into.support@gmail.com

## In short

- Screen Helper uses your microphone and takes a screenshot **only when you press its hotkey** to ask a question.
- Your recording, your screenshot and recent conversation text go **straight from your computer to Google's Gemini API**, using **your own Gemini API key**. They do not pass through FusionCore.
- **FusionCore receives none of your data.** The app has no account, no analytics, no ads, no crash reporting and no update checks. We don't sell data, and the app doesn't collect your contacts, location or payment details.
- The app keeps settings and logs on your computer. Your recordings and screenshots are **not saved** unless you turn saving on. You can turn it off again and delete the files at any time.

## When the app uses your microphone and screen

**Microphone.** The app opens the microphone only after you press the hotkey (Ctrl+Alt+Space by default). In the default "hold" mode it records while you hold the key and stops when you let go. In "toggle" mode you press once to start and again to send. A recording stops by itself after 60 seconds at most. Recordings shorter than 0.4 seconds are thrown away and not sent.

**Screenshot.** When you send a question, the app takes one screenshot of the monitor your mouse is on. If you change the `capture` setting to `"all"`, it captures every monitor. Screenshots are scaled down (by default to at most 1280 pixels on the long side) and converted to JPEG images before they are sent. The app's own pointer and caption are kept out of the screenshot.

**Mouse position.** The app reads where your mouse is so it can pick the right monitor and so its pointer can follow the mouse on screen. Your mouse coordinates are not sent to Google.

**Other data.** The app does not read window titles, the clipboard, files on your computer, or anything else from other apps. The only things it sees on your screen are what is visible in the screenshot.

## What is sent to Google Gemini

Each question sends requests to Google's Gemini API (`generativelanguage.googleapis.com`) over an encrypted HTTPS connection. Your API key is sent in a request header, never in the web address.

- **To understand and answer your question:** your recording (16 kHz mono audio), the screenshot(s) and their pixel size, and the text of up to your last 10 questions and answers (text only, cut to 300 characters each and 2,000 characters in total). By default Gemini writes down what you said and answers in the same request. An optional setting (`"stt": "gemini-transcribe"`) sends the recording in a separate request just to write down what you said.
- **To speak the answer:** the answer text, the chosen voice name and a short speaking-style note. Gemini sends back audio. If you set `"speak": false`, the app shows the answer as text only and doesn't make this request.

Older screenshots and recordings are never sent again. Only the text of earlier questions and answers is sent, as conversation context.

## How Google handles that data

Google processes these requests under its own terms, which apply to your API key and your Google account, not to FusionCore. What Google does with them depends on how the Google project behind your key is set up:

- **Free (unpaid) quota:** Google's Gemini API Additional Terms say Google uses the content you submit and the responses to provide, improve and develop its products, and that human reviewers may read it. Google asks you not to submit sensitive, confidential or personal information on unpaid quota.
- **Paid quota (billing turned on):** the same terms say Google does not use your prompts or responses to improve its products. It keeps them for a limited time to detect abuse and for legal reasons.

Read Google's own pages for the details:

- Gemini API Additional Terms of Service: https://ai.google.dev/gemini-api/terms
- Google Privacy Policy: https://policies.google.com/privacy

## What is stored on your computer

The app stores these files in your user profile, in the `%APPDATA%\screen-helper` folder. The tray menu items "開啟設定檔 config.json" and "開啟記錄資料夾（logs）" open the right place.

| File | What's in it |
|---|---|
| `config.json` | Your settings. If you paste your Gemini API key here, it is stored **in plain text**. You can use the `GEMINI_API_KEY` environment variable instead; if it is set, the app uses it first. |
| `logs\turns-YYYY-MM-DD.jsonl` | One line per question: the time, what Gemini heard you say, the answer, where the pointer went, the models and voice used, timings and any error message. |
| `logs\artifacts\` | **Off by default** (`"save_artifacts": false`): no recordings or screenshots are saved. If you set `"save_artifacts": true` in `config.json`, then for each answered question the app saves your full recording (`.wav`) and the screenshot (`.jpg`, with red circles where the pointer went) in `%APPDATA%\screen-helper\logs\artifacts\`. Set it back to `false` to stop; files already saved stay until you delete them. Note: a `config.json` written by an earlier test build says `true`, so saving stays on there until you change it. |
| `quota.json` | How many requests each Gemini model has used today, so the app can skip models that are used up. It contains no questions or answers. |

The app never writes your API key to the logs.

**Kept in memory only:** the conversation context (your recent questions and answers) and the audio of the last spoken answer (for the "say it again" menu item). Both are gone when you quit the app.

## How long data is kept

- **On your computer:** until you delete it. The app doesn't delete old logs or saved recordings and screenshots by itself.
- **At FusionCore:** nothing is kept, because nothing is sent to us.
- **At Google:** see Google's terms above.

## Windows system voice

If the Gemini voice fails, or the app's local count says today's Gemini voice quota is used up, the app can read the answer aloud with a voice installed in Windows. Windows makes this speech on your computer, and the app doesn't send anything extra for it. To turn it off, set `"system_voice_fallback": false`.

## Your choices

- **Don't want anything recorded or sent?** Don't press the hotkey, or quit the app from the tray menu ("結束 Quit").
- **Save recordings and screenshots, or not:** they are not saved by default. To save them, set `"save_artifacts": true` in `config.json`; to stop, set it to `false` (or delete the line). Save the file and restart the app. The files go to `%APPDATA%\screen-helper\logs\artifacts\`, and you can delete them at any time.
- **Delete local data:** delete the `logs` folder, `quota.json` and `config.json` (with the tray menu items above, or in File Explorer).
- **Stop all use of your key:** remove the key from `config.json`, or revoke it in Google AI Studio.
- **Uninstall:** uninstall Screen Helper from Windows Settings. For the Microsoft Store version, Windows normally keeps the app's files in a private per-app location and removes them on uninstall. If a `screen-helper` folder is still there afterwards, you can delete it yourself.

## Children

Screen Helper is not meant for children. Google's Gemini API terms require users to be 18 or older, and you need your own Gemini API key to use the app.

## Changes to this policy

If the app starts handling data differently, we will update this page and its effective date.

## Contact

FusionCore — bump.into.support@gmail.com
