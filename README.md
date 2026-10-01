# Raquel AI Coding Tutor

Python desktop prototype for learning programming, built by Raquel Cruz with CustomTkinter and a Gemini conversational assistant.

**Portfolio status:** source reviewed and syntax checked; graphical interface and live Gemini requests have not been validated in this review. No screenshot or recording of a local run is linked here yet.

## Purpose and implemented scope

The project explores desktop UI development, prompt engineering, environment-based credential configuration, and background requests to an external AI service. It is an educational prototype, not a production service or an independently evaluated tutor.

Source: [RaquelTutor2.py](RaquelTutor2.py).

- A fixed 900 × 650 desktop window with a chat area, input field, Send button, and Enter shortcut.
- Solve, Explain, Debug, and Practice buttons that insert starter text; the user completes and sends it.
- Keyword heuristics for programming language, task, and student level, combined with a teaching persona in the prompt.
- A Gemini request using `google.generativeai` and the configured model name `gemini-2.5-flash`.
- A worker thread, disabled Send button while waiting, and a 2.5-second local cooldown.
- Missing-key and API-error messages; optional `assets/raquel.png` with a text placeholder when the file is absent.

These are observations from the source, not proof of successful runtime behavior or teaching quality. References to C, Java, Python, HTML, CSS, and JavaScript describe the prompt's intended coverage, not tested capabilities.

## Evidence and verification

| Evidence | Status | What it establishes |
| --- | --- | --- |
| Source and dependency review | Completed for `RaquelTutor2.py` and `requirements.txt` at commit `e38ce7af55311bd516a1b93d75c64b3aa4800234` | Implementation and declared packages are inspectable. |
| Python syntax check | Passed on 2026-10-01 with Python 3.12.14: `python -m py_compile RaquelTutor2.py` | The reviewed file compiles; this does not import dependencies, open the GUI, or call Gemini. |
| Clean dependency installation and import check | Pending | No working package set has been recorded for this review. |
| Local GUI run, without an API key | Pending | Window layout, controls, and missing-key behavior need a desktop check. |
| Live Gemini interaction | Pending | Authentication, model availability, and response handling remain unverified. |
| Screenshot / short screen recording | Pending; no artifact linked | A real local session still needs to be captured. |
| Accuracy of generated explanations and code | Not evaluated | Generated content must be reviewed and tested separately. |

The Python version used for the syntax check is **not** evidence that the complete application works on that version.

### How to add real portfolio evidence

After following the setup below, capture a local session and add actual links here. A screenshot can establish appearance; a recording can additionally show the submitted prompt and response. Neither establishes answer correctness.

Record alongside each artifact:

- Date, repository commit (`git rev-parse HEAD`), OS, and `python --version` from the project environment.
- Installed package versions (`python -m pip freeze`), whether a key was configured, and the model name from the source.
- Steps attempted, actual observations, errors, and pass/fail status.
- The exact submitted prompt and actual returned text, labelled **AI-generated, not independently verified**.
- Any separate verification of suggested code: command, inputs, observed output, and remaining limitations.

Use the environment's Python executable from the commands below when recording versions. Keep API keys, private code, and personal data out of screenshots and logs. If an API request fails, record the failure rather than replacing it with a fabricated successful response. Update the table only when supporting evidence exists.

## Python and prerequisites

- **Suggested starting version: Python 3.12.** Only syntax compilation on Python 3.12.14 was checked here; full runtime compatibility is pending.
- A graphical desktop and Python with Tk support. This is a desktop application, not a web app or notebook UI.
- Git for the clone commands below, or download and extract the repository ZIP.
- Packages declared in [requirements.txt](requirements.txt): `customtkinter`, `Pillow`, and `google-generativeai`.
- Internet access and a valid `GEMINI_API_KEY` for AI replies. Provider access, quota, model availability, and possible charges must be checked for your account.

Dependencies are unpinned, so installations at different times may resolve to different versions. No tested dependency lock or cross-platform compatibility matrix is provided.

## Run locally

Run all commands from the repository root. The explicit virtual-environment Python paths below ensure installation and launch use the same environment; activation is not required.

### Windows — PowerShell

The `py -3.12` command requires the Windows Python launcher and Python 3.12. If unavailable, use the path to your installed Python 3.12 executable.

```powershell
git clone https://github.com/raquelquiterio2014-byte/Raquel-AI-Coding-Tutor.git
cd Raquel-AI-Coding-Tutor
py -3.12 -m venv .venv
.\.venv\Scripts\python.exe --version
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m pip check
.\.venv\Scripts\python.exe -m py_compile RaquelTutor2.py
.\.venv\Scripts\python.exe -c "import tkinter, customtkinter, PIL, google.generativeai; print('Dependency imports OK')"
.\.venv\Scripts\python.exe -m tkinter
```

Close the Tk test window before continuing. A successful import check confirms imports only; the Tk test confirms a basic Tk window can open, not that this application works.

First, try the application without a key:

```powershell
Remove-Item Env:GEMINI_API_KEY -ErrorAction SilentlyContinue
.\.venv\Scripts\python.exe RaquelTutor2.py
```

Close the application, then configure your key for this PowerShell session and relaunch:

```powershell
$env:GEMINI_API_KEY = "YOUR_KEY_HERE"
.\.venv\Scripts\python.exe -c "import os; print('Key configured:', bool(os.getenv('GEMINI_API_KEY')))"
.\.venv\Scripts\python.exe RaquelTutor2.py
```

Replace the placeholder locally. Never commit a real key or share terminal history containing it.

### macOS / Linux — Bash

Use an installed Python 3.12 executable. Some Linux distributions package Tk separately; install the matching Tk support if the Tk check fails.

```bash
git clone https://github.com/raquelquiterio2014-byte/Raquel-AI-Coding-Tutor.git
cd Raquel-AI-Coding-Tutor
python3.12 -m venv .venv
./.venv/bin/python --version
./.venv/bin/python -m pip install -r requirements.txt
./.venv/bin/python -m pip check
./.venv/bin/python -m py_compile RaquelTutor2.py
./.venv/bin/python -c "import tkinter, customtkinter, PIL, google.generativeai; print('Dependency imports OK')"
./.venv/bin/python -m tkinter
```

Close the Tk window. Try the application without a key:

```bash
unset GEMINI_API_KEY
./.venv/bin/python RaquelTutor2.py
```

Close it, then configure the key in the same terminal and relaunch:

```bash
export GEMINI_API_KEY="YOUR_KEY_HERE"
./.venv/bin/python -c "import os; print('Key configured:', bool(os.getenv('GEMINI_API_KEY')))"
./.venv/bin/python RaquelTutor2.py
```

The code reads the key at startup; restart after changing it. A `.env` file is not loaded automatically.

### Manual verification checklist

These are checks to perform, **not results already obtained**:

1. With no key, launch from the repository root. Check the title, chat area, quick buttons, and input field. If the optional avatar is absent, check the text placeholder.
2. Send the example prompt below. The no-key branch is coded to return: `Set GEMINI_API_KEY in your environment before using the AI assistant.` Record whether this actually appears.
3. Complete a quick-button starter text and submit with Enter. Check that empty input is ignored and Send becomes available again after handling a message.
4. Restart with a valid key. Submit the same prompt, observe the waiting state, and record the actual response or error. An error message is not a successful AI interaction.
5. Review any generated explanation. Test suggested code separately in an appropriate environment before calling it correct.

### Troubleshooting

| Symptom | Check / next step |
| --- | --- |
| Missing module | Install requirements using the same virtual-environment interpreter used to launch. |
| Tk import or display error | Verify Tk support and use a graphical desktop; run the Tk test above. |
| Missing-key message | Set the environment variable in the launch terminal and restart the application. |
| API key, quota, or model error | Check provider credentials, account access, quota, and model availability; preserve the observed error in the evidence record. |
| Tutor image not found | The avatar is optional. For your own image, use `assets/raquel.png` and launch from the repository root. |

## Example interaction — illustrative, not a recorded run

**Input to try:**

> Sou iniciante em Python. Explique como percorrer a lista [4, 2, 6, 7], calcular a soma e a média e criar uma lista com os valores maiores que 5.

**Intended response structure:** a beginner-friendly explanation, commented Python code, a walkthrough, and a practice exercise. This describes the prompt's teaching instructions; no Gemini answer was captured or verified for this example.

**Manual acceptance reference:** the sum should be 19, the mean 4.75, and the filtered list `[6, 7]`. These are arithmetic criteria for reviewing the exercise, not a transcript or evidence that the tutor returned a correct answer. Checking these values alone would not validate every claim in a generated explanation.

## Limitations

- AI explanations and code can be incorrect or misleading. The app has no code execution sandbox, automatic answer checking, or measured educational evaluation.
- Chat text stays visible, but prior messages are not included in subsequent API prompts. There is no conversational memory, saved history, or export feature.
- Language, task, and level detection uses substring heuristics, not semantic classification. For example, `javascript` contains `java` and can be classified as Java because the Java check runs first. Several task/level keywords are Portuguese while quick-button starter text is English.
- Requests use a worker thread, but GUI responsiveness, shutdown during a request, and thread-to-GUI behavior have not been tested here. There is no explicit timeout, retry/backoff, or cancellation logic.
- The local cooldown does not guarantee compliance with provider quotas. Error handling uses a broad exception handler and text matching.
- Provider availability and SDK compatibility can change. The configured model name is not proof that an account can access it.
- Prompts are sent to an external AI provider. Do not submit secrets, confidential source code, or personal data.
- The fixed window size and optional relative-path image need layout checks on different screen sizes and scaling settings.
- Importing `RaquelTutor2.py` starts the GUI because there is no main guard. The preflight import command deliberately imports dependencies only.

## Next portfolio milestones

1. Record a clean installation and local no-key session with exact environment versions.
2. Add a screenshot and a short recording of one actual API interaction, with an honestly labelled transcript.
3. Review and independently test suggested code; document both correct results and failures.
4. Use those observations to prioritize future code changes, including detector fixes, dependency reproducibility, and request handling.
