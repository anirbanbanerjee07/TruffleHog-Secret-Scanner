# 🐷🔐 TruffleHog Secret Scanner

**A practical guide to detecting exposed secrets, API keys, passwords, and credentials using TruffleHog on Windows.**

![Platform](https://img.shields.io/badge/Platform-Windows-0078D4?logo=windows&logoColor=white)
![Security](https://img.shields.io/badge/Focus-Secret%20Scanning-red)
![Tool](https://img.shields.io/badge/Tool-TruffleHog-purple)
![License](https://img.shields.io/badge/License-MIT-green)

## 📌 Overview

TruffleHog is an open-source security tool that helps developers identify exposed secrets and credentials in source code, Git repositories, and local files.

This repository documents my hands-on learning journey with TruffleHog, including installation on Windows, configuration through Command Prompt (CMD), scanning local project directories, checking Git history, and understanding security findings.

The goal is to promote secure coding practices and reduce the risk of accidentally exposing sensitive credentials in software projects.

## ✨ Features

- 🔍 Scan local files and directories for exposed secrets.
- 🗂️ Inspect Git repositories and commit history.
- 🔑 Detect potential API keys, tokens, passwords, and other credentials.
- 🪟 Install and use TruffleHog on Windows.
- 💻 Execute security scans using Windows CMD.
- 🛡️ Learn practical secret-management and remediation techniques.
- 📚 Document common errors and troubleshooting steps.

## 🛠️ Technologies & Tools

- **TruffleHog** — Secret detection and scanning.
- **Windows CMD** — Command-line interface.
- **Git & GitHub** — Version control and repository management.
- **Chocolatey** — Optional Windows package manager.
- **GitHub Security Practices** — Secure credential handling.

## 📋 Prerequisites

Before getting started, ensure you have:

- Windows 10 or Windows 11.
- Git installed if you want to scan Git repositories.
- TruffleHog installed and accessible from CMD.
- Access to the local project directory you want to scan.

Check the installations:

```cmd
git --version
trufflehog --version
```

## 🚀 Installation on Windows

### Option 1: Install using Chocolatey

If Chocolatey is installed and its TruffleHog package is available, open CMD as Administrator and run:

```cmd
choco install trufflehog -y
```

If TruffleHog is already installed:

```cmd
choco upgrade trufflehog -y
```

Verify the installation:

```cmd
trufflehog --version
```

### Option 2: Install using the official binary

1. Visit the [official TruffleHog releases](https://github.com/trufflesecurity/trufflehog/releases).
2. Download the appropriate Windows binary archive.
3. Extract the files into `D:\TruffleHog`.
4. Ensure `trufflehog.exe` is inside that directory.
5. Add `D:\TruffleHog` to your Windows user `Path` environment variable if you want to run it from any directory.
6. Open a new CMD window and verify the installation.

```cmd
D:
cd \TruffleHog
trufflehog.exe --version
```

## 🔍 Usage Guide

### 1. Scan a local project directory

Use the filesystem scanner to inspect files and subdirectories.

Example:

```cmd
trufflehog filesystem D:\laravel-workspace\lets-chat-main
```

Replace the path with the directory you want to inspect.

This scan checks local files for potential secrets without requiring the directory to be a Git repository.

### 2. Scan a local Git repository

First, make sure the target directory is an actual Git repository.

```cmd
cd /d D:\laravel-workspace\lets-chat-main
git status
```

If Git recognizes the repository, run the scan from its parent directory:

```cmd
cd /d D:\laravel-workspace
trufflehog git file://lets-chat-main
```

This scans the repository's Git history and applicable staged changes. Review the official documentation for supported repository URL formats and options.

### 3. Scan a public GitHub repository

Only scan repositories you are authorized to assess.

```cmd
trufflehog git https://github.com/OWNER/REPOSITORY
```

Replace `OWNER/REPOSITORY` with the target repository's actual owner and name.

### 4. Display available commands

```cmd
trufflehog --help
```

For filesystem-specific options:

```cmd
trufflehog filesystem --help
```

For Git-specific options:

```cmd
trufflehog git --help
```

## 🧪 Example Workflow

The following workflow can be used when reviewing a development project.

1. Open Windows CMD.
2. Navigate to the project directory.
3. Run a filesystem scan.
4. Review any findings without publishing sensitive values.
5. Investigate whether each finding is a real credential or a false positive.
6. Revoke or rotate exposed credentials when necessary.
7. Move secrets into environment variables or an appropriate secrets manager.
8. Scan again to verify the remediation.

Example:

```cmd
cd /d D:\laravel-workspace\lets-chat-main
trufflehog filesystem D:\laravel-workspace\lets-chat-main
```

**Note:** A filesystem scan and a Git-history scan have different scopes. Use both when appropriate.

## ⚠️ Troubleshooting

### Error: Directory does not appear to be a Git repository

**Cause:** The specified directory is not a Git repository, or the command points to the wrong location.

**Solution:**

```cmd
git -C D:\laravel-workspace\lets-chat-main status
```

If the directory is not a Git repository, use the filesystem scanner instead.

### Error: Access is denied during automatic updates

**Cause:** Windows may prevent the updater from replacing a Chocolatey-managed executable.

**Solution:**

1. Close other running TruffleHog processes.
2. Open CMD as Administrator.
3. If necessary, update TruffleHog through Chocolatey.
4. Retry the scan.

```cmd
choco upgrade trufflehog -y
```

If the issue persists, check Chocolatey permissions and the official installation documentation.

### Error: TruffleHog is not recognized

**Cause:** The executable's directory may not be included in the Windows `Path` environment variable.

**Solution:** Add the directory containing `trufflehog.exe` to your user `Path`, reopen CMD, and run:

```cmd
trufflehog --version
```

## 🛡️ Security Best Practices

- Never commit `.env` files containing real credentials.
- Keep API keys, access tokens, and passwords out of source code.
- Use environment variables or a dedicated secrets manager.
- Add appropriate sensitive files to `.gitignore`.
- Rotate or revoke exposed credentials immediately.
- Remember that deleting a secret from the latest commit does not necessarily remove it from Git history.
- Do not upload raw scan reports containing sensitive values to a public repository.
- Treat unverified findings seriously until they have been investigated.
- Scan only systems and repositories you own or have permission to assess.

**Important:** If a real credential is exposed, removing it from a file is not enough. Revoke or rotate the credential and investigate its potential misuse.

## 📚 Official Resources

- [TruffleHog GitHub Repository](https://github.com/trufflesecurity/trufflehog)
- [Official Releases](https://github.com/trufflesecurity/trufflehog/releases)
- [TruffleHog Documentation](https://docs.trufflesecurity.com/)
- [Git Documentation](https://git-scm.com/doc)
- [GitHub Secret Scanning](https://docs.github.com/en/code-security/secret-scanning/introduction/about-secret-scanning)

## 🎯 Learning Objectives

Through this project, I aim to improve my understanding of:

- Secret detection and credential exposure.
- Git repository security.
- Secure software development practices.
- Windows command-line security tools.
- Credential remediation and prevention.
- Practical application security workflows.

## 🤝 Contributions

Suggestions, corrections, and improvements are welcome.

If you would like to contribute, fork the repository, create a feature branch, and submit a pull request.

## 📄 License

This repository's original documentation is intended to be released under the MIT License. See [LICENSE](LICENSE) for details.

TruffleHog is a separate project maintained by Truffle Security. Refer to its official repository for its licensing terms.

## 👨‍💻 Author

**Anirban Banerjee**

GitHub: [@anirbanbanerjee07](https://github.com/anirbanbanerjee07)

---

⭐ If this guide helps you learn about secret scanning and secure coding, consider starring the repository.

**Disclaimer:** This repository is intended for educational and defensive security purposes. Scan only systems, files, and repositories you own or are authorized to assess.
