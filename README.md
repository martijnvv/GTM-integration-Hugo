# GTM-integration-Hugo
Google Tag Manager integration for Hugo static websites

Please read the detailed instruction on how to implement on my blog: [How to add Google Tag Manager to a Hugo static website](https:///martijnvanvreeden.nl/how-to-add-google-tag-manager-to-hugo-static-website/)

## TL;DR
Merge this repo with your Hugo folder struture (either as a submodule or manually). Adjust paths if required. 

In the layout/template file/partial of the site's `<head>` section add the following lines, preferably directly underneath the `meta charset` elements:

```
{{ if .Site.Params.gtm_datalayer }}{{ partial "gtm-datalayer.html" . }}{{ end }}
{{ if .Site.Params.gtm_id}}{{ partial "gtm-js-snippet.html" . }}{{ end }}
```

For the second GTM (noscript) snippet (for browsers with disabled/blocked javascript), add the following Hugo code directly underneath the opening `<body>` tag of your site's template/partial file:

```
{{ if not .Site.IsServer}}{{ if .Site.Params.gtm_id}}{{ partial "gtm-noscript-snippet.html" . }}{{ end }}{{ end }}
```

Note that this snippet by default is disabled when in Hugo's server mode (during development), feel free to adjust if needed.

## Updates:

* 26-06-2022: Add support for one GTM environment (for staging/development), which activates when HUGO_ENVIRONMENT does not equal `production`

* 04-05-2021: Included additional site param to manage a custom endpoint for Server Side GTM "gtm_endpoint" 
