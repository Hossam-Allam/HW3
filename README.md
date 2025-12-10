# CMPE341 – HW3

## Homework: PokéCLI — Pokémon Data Explorer (Bash + curl + jq)

This homework requires you to build a Bash script (`pokecli.sh`) that interacts with the PokéAPI (`https://pokeapi.co/`).  
You will create an interactive CLI tool that can look up Pokémon, compare them, and manage a local “team” stored in a file.

Your submission must include:

- `pokecli.sh`
- `README.md` explaining usage and examples

---

## Task 0 — Setup and Requirements

At the start of your script, check for the required tools:

```bash
command -v curl >/dev/null 2>&1 || { echo "curl is required"; exit 1; }
command -v jq   >/dev/null 2>&1 || { echo "jq is required";   exit 1; }
```

All API requests follow this format:

```
https://pokeapi.co/api/v2/pokemon/<name-or-id>
```

Your script must include a main loop with a menu:

```
1) Look up a Pokémon
2) Compare two Pokémon
3) Manage team
4) Exit
```

---

## Task 1 — Single Pokémon Lookup

Implement a feature that:

1. Asks the user for a Pokémon name or ID.
2. Fetches its data using `curl -s`.
3. Validates the result (handle invalid or missing Pokémon).
4. Extracts the following with `jq`:
   - name
   - id
   - types
   - height, weight
   - base stats (HP, Attack, Defense, Sp. Attack, Sp. Defense, Speed)
5. Prints the information in a clear format.

---

## Task 2 — Pokémon Comparison

Implement a comparison feature that:

1. Prompts for two Pokémon names or IDs.
2. Fetches and validates both.
3. Extracts their base stats.
4. Prints a side-by-side comparison table, indicating which Pokémon has the higher value for each stat.

Example structure:

```
Stat         A        B        Winner
HP           ...      ...      ...
Attack       ...      ...      ...
Defense      ...      ...      ...
Speed        ...      ...      ...
```

---

## Task 3 — Team Management (team.txt)

Create a submenu:

```
1) View team
2) Add Pokémon
3) Remove Pokémon
4) Team summary
5) Back
```

### Requirements

#### View Team

- If `team.txt` does not exist or is empty, print a message.
- Otherwise list team members with numbering.

#### Add Pokémon

- Maximum team size: 6.
- Validate the Pokémon using the API before adding.
- Append valid entries to `team.txt`.

#### Remove Pokémon

- Display the indexed list.
- Ask for the index to remove.
- Delete that line from the file.

#### Team Summary

For each Pokémon in `team.txt`:

1. Fetch stats with the API.
2. Compute average values for at least:
   - HP
   - Attack
   - Defense
   - Speed

Print a short summary report.

---

## Task 4 — Main Program Structure

Your script must:

- Use a continuous loop until the user selects “Exit”.
- Validate all menu input.
- Handle invalid API responses or user mistakes without crashing.
- Keep functions modular (e.g., `lookup_pokemon()`, `compare_pokemon()`, `team_menu()`).

---

## Submission

Submit:

- `pokecli.sh`
- `README.md` containing:
  - description of the script
  - instructions for running
  - sample outputs
