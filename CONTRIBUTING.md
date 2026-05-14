# Contributing to HELIO Pro

Thank you for your interest in improving HELIO Pro.

## Reporting Bugs

1. Open an [Issue](https://github.com/sjm208/Helio-Pro/issues)
2. Include the contents of `helio_pro.log` (created in the same folder as the script)
3. Describe your capture setup (camera, number of images, OS, Python version)

## Suggesting Features

Open an Issue with the label `enhancement`. Describe:
- What problem it solves
- Which type of object or workflow it benefits
- Whether you'd be able to test it

## Pull Requests

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Test on at least one real capture before submitting
4. Submit a pull request with a clear description

## Code Style

- Follow PEP 8 broadly
- All Tkinter variable reads must happen on the main thread (see existing `_engine_snap` patterns)
- Heavy operations must run in `threading.Thread(daemon=True)`
- Add a tooltip to every new button

## Contact

HELIO Pro —   
https://github.com/sjm208/Helio-Pro
