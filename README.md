# PhishGuard AI

PhishGuard AI is a Flask web application for examining potentially suspicious URLs, email text, and SMS messages. It applies transparent, rule-based checks to identify common phishing indicators, assigns a risk score and threat level, and can generate a PDF summary of an analysis.

This project is intended for cybersecurity education and awareness. Its results are heuristic signals, not a definitive verdict about whether content is safe or malicious.

## Contents

- [Features](#features)
- [Technology](#technology)
- [Project Structure](#project-structure)
- [Requirements](#requirements)
- [Installation and Setup](#installation-and-setup)
- [Using the Application](#using-the-application)
- [Detection Method](#detection-method)
- [Privacy and Limitations](#privacy-and-limitations)
- [Project Objectives](#project-objectives)
- [Potential Future Work](#potential-future-work)
- [Contributing](#contributing)
- [Author](#author)
- [License](#license)

## Features

- Analyze URLs for suspicious structural and textual indicators.
- Analyze email and SMS text for a set of suspicious words and phrases.
- View a risk score, threat level, and the reasons that contributed to the result.
- Review general security recommendations after an analysis.
- Download a PDF analysis report.
- Use the application through a browser-based interface with no database setup.

## Technology

- **Backend:** Python, Flask
- **Frontend:** HTML, CSS, JavaScript, Jinja templates
- **URL validation dependency:** `validators`
- **PDF reports:** ReportLab

## Project Structure

```text
PhishGuard-AI/
├── analyzer/
│   ├── __init__.py
│   ├── email_checker.py
│   ├── report_generator.py
│   ├── risk_engine.py
│   ├── sms_checker.py
│   └── url_checker.py
├── static/
│   ├── css/
│   │   └── style.css
│   ├── images/
│   └── js/
│       └── script.js
├── templates/
│   ├── about.html
│   ├── analyzer.html
│   ├── contact.html
│   ├── footer.html
│   ├── index.html
│   ├── navbar.html
│   └── result.html
├── app.py
├── requirements.txt
└── README.md
```

## Requirements

- Python 3.8 or newer
- `pip`

The exact Python version used for development is not pinned in this repository. The required Python packages and versions are listed in `requirements.txt`.

## Installation and Setup

Open a terminal in the project directory. If you have not already downloaded or cloned the project, use the repository URL provided by its host.

Create and activate a virtual environment.

**Windows PowerShell:**

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**Windows Command Prompt:**

```bat
py -m venv .venv
.venv\Scripts\activate.bat
```

**macOS or Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install dependencies and start the development server:

```bash
python -m pip install -r requirements.txt
python app.py
```

Visit [http://127.0.0.1:5000](http://127.0.0.1:5000) in your browser. Stop the server with `Ctrl+C` in the terminal.

## Using the Application

1. Open the home page and navigate to the analyzer.
2. Select URL, email, or SMS analysis.
3. Enter the URL or message text and submit it for analysis.
4. Review the score, threat level, detection reasons, and security recommendations.
5. Use the report option to download a PDF summary.

The application also provides About and Contact pages. The main routes are `/`, `/analyzer`, `/about`, and `/contact`; analysis is submitted to `/analyze`.

## Detection Method

The application uses deterministic checks implemented in the `analyzer/` package. It does not currently use a trained machine-learning model or query an external threat-intelligence service.

- **URLs:** Checks include the use of HTTP instead of HTTPS, IP addresses, `@` characters, URL length, dots and subdomains, hyphens and digits in the domain, known URL shorteners, selected keywords, encoded characters, path and parameter length, and a small list of flagged top-level domains.
- **Email text:** Looks for a fixed set of words and phrases such as urgent requests, password or account language, and references to clicking or prizes.
- **SMS text:** Looks for a fixed set of keywords associated with OTPs, prizes, urgency, verification, claims, and banking.

Each matching rule adds points. Scores are capped at 100 and mapped to these levels:

| Score | Threat level |
| --- | --- |
| 0–39 | Low |
| 40–59 | Medium |
| 60–79 | High |
| 80–100 | Critical |

The rules can produce false positives and false negatives. A low score does not establish that a message or website is safe, and a high score is not proof of malicious intent.

## Privacy and Limitations

- No database or account system is configured by this project.
- Submitted content is processed by the local Flask application to render a result. Avoid using sensitive or confidential content unless you have reviewed and accepted your local environment's handling of it.
- The checks are based on fixed heuristics and may not recognize new or carefully disguised phishing attempts.
- The application does not fetch or inspect the destination website, verify sender identity, scan attachments, or provide real-time reputation results.
- The built-in Flask server runs with debug mode enabled and is intended for local development only. Do not expose it to the public internet or use it as a production deployment without appropriate security and deployment changes.

## Project Objectives

- Demonstrate rule-based phishing indicator analysis.
- Support cybersecurity awareness and safer online practices.
- Provide an approachable interface for reviewing suspicious URLs and messages.
- Explain which indicators contributed to an analysis result.

## Potential Future Work

- Add carefully evaluated machine-learning detection with documented datasets and performance metrics.
- Integrate reputable URL and domain intelligence services.
- Add safe email attachment analysis.
- Create a browser extension or analysis history dashboard.
- Add production deployment configuration and security hardening.

## Contributing

Contributions and suggestions are welcome. For a code contribution, fork the repository, make a focused change, test it locally, and submit a pull request through the repository host. Include a clear description of behavior changes and any known limitations.

## Author

**Muhammad Aqeel**

## License

No license has been specified for this project. All rights and permissions remain with the respective copyright holder unless a license is added to the repository.
