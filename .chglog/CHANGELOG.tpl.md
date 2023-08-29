{{ range .Versions }}

## {{ if .Tag.Previous }}[{{ .Tag.Name }}]({{ $.Info.RepositoryURL }}/compare/{{ .Tag.Previous.Name }}...{{ .Tag.Name }}){{ else }}[{{ .Tag.Name }}]({{ $.Info.RepositoryURL }}/commits/{{ .Tag.Name }}){{ end }} ({{ datetime "2006-01-02" .Tag.Date }})

{{ if .NoteGroups -}}
{{ range .NoteGroups -}}

### {{ if eq .Title "BREAKING CHANGE" }}⚠️{{ .Title }}{{ else }}{{ .Title }}{{ end }}

{{ range .Notes }}
{{ .Body }}
{{ end }}
{{ end -}}
{{ end -}}

{{ range .CommitGroups -}}

### {{ .Title }}

{{ range .Commits -}}

- {{ if .Scope }}**{{ .Scope }}:** {{ end }}{{ .Subject }} by **@{{.Author.Name}}** in [{{.Hash.Short}}]({{ $.Info.RepositoryURL }}/commit/{{.Hash.Long}})
{{ end }}

{{ end -}}

{{- if .RevertCommits -}}

### Reverts

{{ range .RevertCommits -}}

- {{ .Revert.Header }}
{{ end }}

{{ end -}}

{{- if .MergeCommits -}}

### Pull Requests

{{ range .MergeCommits -}}

- {{ .Header }}
{{ end }}
{{ end -}}

### Full Changelog: {{ if .Tag.Previous }}[{{ .Tag.Previous.Name }} -> {{ .Tag.Name }}]({{ $.Info.RepositoryURL }}/compare/{{ .Tag.Previous.Name }}...{{ .Tag.Name }}){{else}}[{{ .Tag.Name }}]({{ $.Info.RepositoryURL }}/commits/{{ .Tag.Name }}){{ end }}

{{- end -}}
