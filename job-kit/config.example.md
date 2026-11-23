# job-kit config

Copy this file to your jobs folder as `job-kit.config.md` and fill it in. It holds your personal details, so keep it out of any public repository.

name: Alex Example
city: City
phone: 050-000-0000            # used exactly as written
email: name@example.com
linkedin: linkedin.com/in/example
github:                        # leave empty if not active

jobs_folder: /path/to/Jobs
master: Resume - Master.md     # source of truth, relative to jobs_folder
private_marker: "Private Working Notes"   # content below this line is private
general_resume: Resume - Name.pdf
template: templates/resume-template.html  # your copy of the design
profiles: profiles/            # your domain profiles
market: israel                 # israel | default
page_limit: 1
documents_language: English

current_title_line: "Current Title, Group (Previous Title until <date>)"

banned_phrases:
  - "from design to production"
  - "owns end to end"

design_notes: |
  Describe your design rules here (fonts, colours, header graphic) so the skill keeps them.

personal_rules: |
  Any extra rules, for example: tailoring stays subtle; no sentence aimed at a specific company.
