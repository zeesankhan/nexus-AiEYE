# Security

NEXUS AiEYE is a local-first geospatial visualization project designed for
exploration, education, research, demonstrations, and experimentation.

It works with publicly available data and third-party services. It is not
intended to be a hardened production security platform.

This document explains the project's security practices and how to report
security issues responsibly.

---

## Reporting a Vulnerability

Please report potential security vulnerabilities privately rather than
publishing exploitable details in a public GitHub issue.

Use GitHub's private vulnerability reporting feature:

**Repository:**
https://github.com/zeesankhan/nexus-AiEYE

Open the repository's **Security** tab and select **Report a vulnerability**
if private vulnerability reporting is enabled.

When reporting an issue, please provide:

* A clear description of the vulnerability
* Steps required to reproduce it
* The affected file or component
* Potential security impact
* Any relevant logs or screenshots
* A suggested mitigation, if available

Please do not include private API keys, passwords, authentication tokens, or
other sensitive credentials in a report.

Security researchers who responsibly disclose vulnerabilities may be credited
in the project's release notes or security acknowledgements, with permission.

---

## Secrets and API Keys

**Never commit private credentials to this repository.**

Secret API keys and authentication credentials should remain outside the
client-side application whenever possible.

Recommended practices include:

* Store secrets in environment variables.
* Keep `.env` files out of version control.
* Commit only `.env.example` files containing placeholder values.
* Never place private API keys directly inside JavaScript or HTML source.
* Rotate a credential immediately if it is accidentally exposed.
* Use provider-side restrictions and usage limits wherever available.

### Client-Side Credentials

Some services require a public/client-side token because the browser connects
directly to the provider.

Client-side credentials should be treated as **public credentials**, not
secrets.

Where supported, restrict them using:

* HTTP referrer restrictions
* API/service restrictions
* Domain restrictions
* Usage quotas
* Provider-side billing limits

A key that is intentionally exposed to a browser cannot be made completely
secret through JavaScript obfuscation.

---

## Third-Party Services

NEXUS AiEYE may communicate with external services and public APIs.

Examples may include:

* Cesium
* Google Maps
* OpenStreetMap
* NASA
* USGS
* OpenSky Network
* CelesTrak
* Open-Meteo
* Radio Browser
* Other public data providers

Each provider has its own security requirements, rate limits, privacy
policies, licenses, and terms of service.

Users are responsible for configuring credentials and using these services in
accordance with their respective requirements.

---

## Local Development Server

NEXUS AiEYE uses a development/preview server for local development.

For normal development, keep the server accessible only from the local
machine whenever possible.

If you intentionally expose the development server to another device or
network, understand that any server-side API functionality may become
accessible to other users on that network.

Do not expose a development server containing private credentials to the
public internet.

For production deployments, use an appropriately secured application server,
authentication layer, reverse proxy, firewall, and provider-side access
controls.

---

## API Proxy Security

Where the application uses server-side proxy endpoints, those endpoints should
follow these principles:

* Do not accept arbitrary upstream URLs when they are not required.
* Restrict upstream requests to known and trusted providers.
* Validate user-controlled parameters.
* Reject malformed or unexpected requests.
* Apply reasonable request and response limits.
* Use connection and request timeouts.
* Avoid exposing internal errors or credentials to clients.
* Do not log authentication credentials.
* Avoid returning unnecessary upstream response data.
* Apply rate limiting to expensive or abuse-prone endpoints where appropriate.

These protections help reduce risks such as SSRF, credential exposure, resource
exhaustion, and unintended third-party API usage.

---

## Data Handling

NEXUS AiEYE is primarily a visualization layer for geographic and
publicly available information.

Data displayed by the application may be:

* Delayed
* Incomplete
* Inaccurate
* Temporarily unavailable
* Supplied by third-party services
* Subject to provider-specific limitations

The application should not be treated as an authoritative source of
real-world intelligence.

---

## Privacy

NEXUS AiEYE may connect to third-party services when specific features are
enabled.

Those services may receive technical information such as:

* IP addresses
* Browser information
* Requests made to their APIs
* Information necessary to provide the requested service

Third-party services may have their own logging and privacy practices.

Users should review the applicable provider policies before enabling features
that communicate with external services.

Do not enter passwords, private credentials, personal identification
information, or other sensitive information into the application unless the
specific feature explicitly requires it and appropriate protection is in
place.

---

## Dependency Security

NEXUS AiEYE depends on third-party libraries and packages.

Before updating dependencies:

1. Review the package changes.
2. Check for known security advisories.
3. Test the application locally.
4. Avoid installing packages from untrusted sources.

Keep the project's dependencies reasonably up to date and remove packages
that are no longer required.

---

## Repository Security

Contributors should take care not to commit:

* API keys
* Access tokens
* Passwords
* Private certificates
* `.env` files containing secrets
* Personal information
* Private datasets
* Authentication cookies
* Provider credentials

Before pushing changes to GitHub, review the staged files with:

```bash
git status
```

and inspect changes with:

```bash
git diff --cached
```

---

## Third-Party Data and Assets

Public data does not necessarily mean unrestricted data.

Datasets, maps, imagery, 3D models, fonts, APIs, and other external assets
may have individual licensing and attribution requirements.

Users must follow the applicable terms of the original provider.

See:

`DATA_SOURCES.md`

for information about data sources used by the project.

---

## Responsible Use

NEXUS AiEYE is intended for:

* Education
* Research
* Visualization
* Development
* Demonstrations
* Exploration of publicly available information

Users should respect privacy, applicable laws, data-provider terms, and
third-party licenses.

Publicly available information should not automatically be treated as
verified, complete, or authoritative intelligence.

---

## Security Updates

Security-related improvements may be included in normal project updates.

If a vulnerability affects users of a released version, appropriate
information may be added to the repository's security documentation or
release notes.

---

## Maintainer

**NEXUS AiEYE**

GitHub repository:

https://github.com/zeesankhan/nexus-AiEYE

---

## License

The project's source-code license is described in:

`LICENSE`

Third-party components and data may be governed by separate licenses and
terms.
