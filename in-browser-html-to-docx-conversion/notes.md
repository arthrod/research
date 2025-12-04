# Notes

## Setup
- Created directory structure.
- Updated `.gitignore` to prevent tracking of library code (avoiding file limits and repo bloat).
- Installed packages using `npm install`.
- Moved packages to individual folders for analysis.

## Analysis Process
- Used a Python script (`gather_info.py`) to crawl the directories and gather file lists and sizes.
- Used `generate_analysis.py` to create `analysis.md` summarizing each package (version, main file, size, file list).
- Used `compare.py` to run a tournament-style comparison based on heuristics:
    - Documentation quality (README size)
    - TypeScript support
    - Test existence
    - Version/Maintenance
    - Relevance (penalizing non-converters like type definitions or specific editor plugins if they are not general purpose).

## Findings
- Many packages are forks of `html-docx-js`.
- `@turbodocx/html-to-docx` emerged as the winner due to superior documentation, modern versioning, and full TypeScript support.
- `html-docx-js-typescript` was a strong runner-up.

## Deliverables
- `files_list.md`: List of all packages.
- `analysis.md`: Detailed breakdown of each package.
- `comparison_notes.md`: Log of the comparison tournament.
- `README.md`: Final report.
