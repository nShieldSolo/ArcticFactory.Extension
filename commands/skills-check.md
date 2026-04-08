---
id: "speckit.arc.skills-check"
name: "Skills Check"
description: "Kiểm tra và cài đặt các Skills cần thiết cho project"
---

# /speckit.arc.skills-check

You are an expert AI developer assistant responsible for automating the environment setup and skill management for the current project.

## Task Specification
Your primary objective is to dynamically read a configuration file containing required Skills and execute the necessary terminal commands to install them. 
**CRITICAL: All your chat responses, progress reports, and final output must be written entirely in Vietnamese.**

## Step-by-Step Instructions

1. **Locate Configuration:** Search for the `skills.json` configuration file at the root directory of the current project (or inside the `.specify/` folder).
2. **Handle Missing Configuration:** If `skills.json` does not exist, immediately create a new `skills.json` file at the root of the project with the following default template:
   ```json
   [
     {
       "repo": "https://github.com/anthropics/skills",
       "skill": "xlsx",
       "agent": "antigravity"
     }
   ]
   ```
3. **Read Data:** Parse the JSON data from the configuration file.
4. **Execute Commands:** Iterate through each skill object in the JSON array. For each skill, use your bash/terminal tools to execute the exact installation command:
   `npx skills add <repo> --skill <skill> -y -a <agent>`
   *(For example, using the template above, you would run: `npx skills add https://github.com/anthropics/skills --skill xlsx -y -a antigravity`)*
5. **Wait to Complete:** Ensure you wait for the terminal command to finish successfully before moving on to the next.

## Output Requirements (in Vietnamese)

Generate a clean and structured summary report in **Vietnamese** containing:
- The total number of Skills found and prepared for installation.
- A bulleted list representing the installation result for each Skill. Use emojis to indicate success/failure (e.g., "✅ Cài đặt thành công skill `xlsx`" or "❌ Cài đặt thất bại skill `xlsx`").

## Quality & Validation Criteria
- Terminal commands MUST be actually executed, not just simulated.
- Error handling: If a command fails, report the error briefly in Vietnamese but continue to the next skill if possible.
- The final response provided to the user must be exclusively in Vietnamese.
