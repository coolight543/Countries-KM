# GitHub Copilot instructions — Countries (small Java Swing demo)

## Quick overview ✅
- This is a small educational Java Swing app that displays country images and lets a user "review" or "quiz" on country data.
- Key files:
  - `Main.java` — program entrypoint; GUI + logic; loads CSV, manages `Country[]` (length 10), handles buttons.
  - `Country.java` — currently a skeleton; should contain fields and basic accessors and `toString()`.
  - `countries-data.csv` — data source (no header): one row per country.
  - image files (e.g. `China.jpg`) — used by `Main` for the display.

## Data format / conventions 📄
- CSV format per line: `CountryName,Capital,PrimaryLanguage,ImageFile`
  - Example: `United States,Washington D.C.,English,US.jpg`
- `Main` expects exactly 10 entries and creates a fixed-size `Country[]` of length 10.
- Filenames are case-sensitive and referenced directly by `ImageIcon`.

## Important implementation notes (code-level) 🔧
- Implement `Country` with private fields: `name`, `capital`, `language`, `imageFile`; provide a 4-arg constructor, getters, and `toString()` that returns e.g. "<country>'s capital is <capital> and its primary language is <language>."
- When parsing CSV lines in `loadCountries()` prefer `line.split(",", 4)` to allow commas in later fields and to get exactly 4 parts.
- `Main` currently uses absolute paths: e.g. `/workspaces/Countries/workspace/countries-data.csv` and `/workspaces/Countries/workspace/<image>`. Be aware this is environment-dependent — either update to relative paths (`new File("countries-data.csv")`) or detect `System.getProperty("user.dir")`.
- `showCountry()` should fetch the image filename from the `Country` object (via `getImageFile()`), build an `ImageIcon` using the same resource directory, and call `imageLabel.setIcon(img)`.
- `nextButtonClick()` should increment `index`, wrap around at 10 (`if (index > 9) index = 0;`), clear `outputLabel`, and call `showCountry()`.
- `reviewButtonClick()` should call the current `Country`'s `toString()`, `System.out.println(...)`, and `outputLabel.setText(...)`.
- `quizButtonClick()` currently uses `Scanner(System.in)` (console input) while the app is a GUI — note this is the existing behavior. If converting to a GUI-only flow, use `JOptionPane.showInputDialog()` and `JOptionPane.showMessageDialog()`.

## How to build & run locally ▶️
- From `workspace/` directory:
  - Compile: `javac Country.java Main.java`
  - Run: `java Main`
- If you see missing file exceptions, check the absolute path constants in `Main.java` and either run from the directory those paths expect or change the code to use relative paths.

## Concrete, prioritized tasks for an AI agent 🛠️
1. Implement `Country.java` (constructor, getters, `toString()`).
2. Implement `loadCountries()` using `split(",", 4)`, instantiate `Country`, and populate `countryArray` (indices 0..9).
3. Implement `showCountry()`, `nextButtonClick()`, `reviewButtonClick()`, `quizButtonClick()` as described above.
4. Optionally: replace hard-coded absolute paths with relative path resolution or configurable constant (note: mention change in PR description).
5. Add a short `README.md` with run instructions and small tests or a verification main (optional).

## Edge-cases & gotchas ⚠️
- The CSV has no header and assumes 10 rows — code should either validate count or fail clearly.
- Mixing console `Scanner(System.in)` with a Swing GUI causes a blocking console read (current behaviour).
- Images must be present in the same directory as the `.java` files at runtime; paths must match exactly.

---
If anything in the above is unclear or you want me to enforce conventions (e.g. switch to relative paths or convert quiz to dialogs), tell me which option you prefer and I’ll make a focused PR.  

<!-- Generated to help AI coding agents be immediately productive in this repository -->