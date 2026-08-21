# Spike Web Solutions — Claude Code plugin marketplace

One namespace for every Claude Code plugin published by
[Spike Web Solutions](https://github.com/spike-web-solutions). Each plugin lives
in its own repository; this repo only holds the marketplace manifest that points
at them.

## Use it

```bash
claude plugin marketplace add spike-web-solutions/claude-plugins
claude plugin install <plugin>@spike-web-solutions
```

Inside a Claude Code session, the same thing:

```
/plugin marketplace add spike-web-solutions/claude-plugins
/plugin install windows-server-admin@spike-web-solutions
```

Update later with:

```bash
claude plugin marketplace update spike-web-solutions
```

## Plugins

| Plugin | Install | What it does |
| --- | --- | --- |
| [windows-server-admin](https://github.com/spike-web-solutions/windows-server-admin) | `windows-server-admin@spike-web-solutions` | 34 skills, 6 commands and 3 agents for Windows Server 2016-2025 administration and the PowerShell that does it. |
| [java-developer](https://github.com/spike-web-solutions/java-developer) | `java-developer@spike-web-solutions` | 14 skills for Java and Spring Framework work, written against Spring Boot 4.1 and Java 21/25 LTS. |

## Adding a plugin

1. Publish the plugin repo with a valid `.claude-plugin/plugin.json` at its root.
2. Append an entry to `plugins` in
   [.claude-plugin/marketplace.json](.claude-plugin/marketplace.json):

   ```json
   {
     "name": "my-plugin",
     "source": { "source": "github", "repo": "spike-web-solutions/my-plugin" },
     "description": "One sentence, present tense, no marketing.",
     "version": "0.1.0",
     "license": "MIT",
     "category": "devops"
   }
   ```

3. Keep `name` stable forever — renaming it breaks every existing install, which
   then has to be uninstalled and reinstalled by hand.
4. Add a row to the table above.
5. Validate before pushing:

   ```bash
   python3 -c "import json;json.load(open('.claude-plugin/marketplace.json'))"
   claude plugin marketplace add ./claude-plugins
   claude plugin marketplace info spike-web-solutions
   ```

## Rules

- `name` at the top of the manifest is the namespace users type after `@`. It is
  not the repo name and does not have to match it.
- A plugin's `version` here should track the `version` in that plugin's own
  `plugin.json`. They are separate files; nothing syncs them automatically.
- Plugin repos may keep their own development marketplace for local clones, but
  it must use a different `name` (for example `windows-server-admin-dev`) so it
  never competes with this one.

## License

MIT
