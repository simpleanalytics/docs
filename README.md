<a href="https://simpleanalytics.com/?ref=github.com/simpleanalytics/docs">
  <img src="https://assets.simpleanalytics.com/images/logos/logo-github-readme.png" alt="Simple Analytics logo" align="right" height="62" />
</a>

# Documentation

Please submit PRs for everything including grammar errors :smile:

## Run on your computer

```
bundle exec jekyll serve
```

## Tools of the MCP server and Tools API

The [tools page](https://docs.simpleanalytics.com/tools) is made from `_data/tools.json`, the list our API returns. Update it after tools change:

```
curl -s https://dashboard.simpleanalytics.com/api/v1/tools > _data/tools.json
```

`_data/tool_groups.yml` puts the tools under headings. A tool that's in no group shows under "Other tools".
