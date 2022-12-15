# GTM-integration-Hugo
Google Tag Manager integration for Hugo static websites, with inspiration and initial code kindly borrowed from Martijn van Vreeden. Please read his blog post on the topic for reference: [How to add Google Tag Manager to a Hugo static website](https:///martijnvanvreeden.nl/how-to-add-google-tag-manager-to-hugo-static-website/)

## Installation
Merge this repo with your Hugo folder structure (either as a submodule or manually). Adjust paths if required. 

In the layout/template file/partial of the site's `<head>` section add the following lines, preferably directly underneath the `meta charset` tag:

```
{{- if eq .Site.Params.gtm_datalayer "basic"}}{{ partial "gtm-datalayer.html" . }}{{ end }}
{{ if .Site.Params.gtm_id}}{{ partial "gtm-js.html" . }}{{ end }}
```

For the second GTM (noscript) snippet (for browsers with disabled/blocked javascript), add the following Hugo code directly underneath the opening `<body>` tag of your site's template/partial file:

```
{{ if not .Site.IsServer}}{{ if .Site.Params.gtm_id}}{{ partial "gtm-noscript.html" . }}{{ end }}{{ end }}
```

Note that this snippet by default is disabled when in Hugo's server mode (during development), feel free to adjust if needed.

## Updates:

### `15-12-2022`
- Add support for [Simo Ahava's excellent ssGTM GTM Loader client template](https://github.com/gtm-templates-simo-ahava/gtm-loader) which allows for changing the gtm.js library name and removing the GTM-XXXXXX id from the GTM snippet if configured in the ssGTM client settings.
- Fix incorrect hugo shortcodes references in README
- Separate datalayer code into separate file for easier management

### `26-06-2022`
- Add support for one GTM environment (for staging/development), which activates when `HUGO_ENVIRONMENT <> production`

### `04-05-2021`
- Include additional site parameters to manage a custom endpoint for Server Side GTM "gtm_endpoint" 
