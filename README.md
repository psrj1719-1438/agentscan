# AgentScan

Identifying potential automation patterns in GitHub accounts

I didn’t expect to build this website, but ended up creating it in a weekend after reading [this article](https://socket.dev/blog/ai-agent-lands-prs-in-major-oss-projects-targets-maintainers-via-cold-outreach) about open source projects being targeted by AI agents.

**This is an ongoing experiment**. It uses an opinionated scoring system to analyze public GitHub events and classify accounts as human, suspicious, or likely bot.
The results are indicators, not verdicts. There’s no AI involved, just event analysis looking for patterns that feel a little off.

<img width="702" height="985" alt="Screenshot 2026-02-24 at 17 08 25" src="https://github.com/user-attachments/assets/b5b2fc89-fedf-410f-84fa-62b8f0f33bee" />


### Contribute
Feel free to contribute to the project!

The stack is a straightforward Nuxt app with a single API endpoint that fetches public data from the GitHub API.

To make things reusable, the core analysis logic lives in a separate package — you can check it out [here](https://github.com/MatteoGabriele/voight-kampff-test), but it might change in the future. Still a working-progress.

This repository mainly focuses on the UI and the GitHub API integration.


### Issues and features requests

Please drop an issue, if you find something that doesn't work, or have an idea for something that works better.

